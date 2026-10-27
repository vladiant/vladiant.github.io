---
layout: post
title: "GPU API Comparison"
date: 2026-10-27
tags: c++ ai coding performance vision
---

## One Algorithm, Four GPU APIs: CUDA vs OpenCL vs Vulkan vs OpenGL Compute

I recently did something slightly masochistic: I implemented the same image-processing algorithm — Gooch et al.'s **Color2Gray** salience-preserving grayscale conversion — in four different GPU compute stacks, plus two CPU baselines. Same algorithm, same input image, same parameters, same machine. Then I measured all of them and, more importantly, paid attention to how it *felt* to write and run each one.

## The workload

Color2Gray's expensive step is `calc_d`: for every pixel it accumulates a signed perceptual difference against **every other pixel** — an *O(N²)* pass. For a 512×512 Lena (262,144 pixels) that's ~69 billion pixel-pair evaluations. On a CPU it's brutal; on a GPU it's embarrassingly parallel. The test hardware is deliberately humble: an **NVIDIA GeForce GTX 750 Ti** (Maxwell, `sm_50`), driver 580.

## The numbers first

| Backend     | Device | Time (ms) | Peak host mem (MB) | GPU util. |
| ----------- | ------ | --------: | -----------------: | --------: |
| BMP (CPU)   | CPU    |   681 698 |               10.2 | —         |
| OpenCV (CPU)| CPU    |   718 382 |               92.7 | —         |
| **Vulkan**  | GPU    | **7 162** |               72.2 | 100%      |
| **CUDA**    | GPU    | **7 962** |               74.7 | 100%      |
| OpenGL CS   | GPU    |     8 871 |              126.3 | 100%      |
| OpenCL      | GPU    |    11 347 |              108.6 | 100%      |
| OpenGL      | GPU    |    12 927 |               71.6 | 100%      |

The headline: moving `calc_d` onto the GPU turns an **11-minute** job into a **7–13 second** one — a 50–95× speedup on a budget card. Every GPU backend pegged the device at 100%, so the bottleneck is raw compute, not API overhead. The spread between GPU backends is small and says more about kernel tuning than about any API being fundamentally faster.

## CUDA — the comfortable one

CUDA gets out of your way. Kernels are C++ with a `__global__` qualifier, launched with `<<<grid, block>>>`, in the same language as the host. The GPU layer was the smallest of the serious ones (~380 lines), and the tooling (Nsight, `compute-sanitizer`, in-kernel `printf`) is best in class.

The catch is **vendor and toolchain lock-in**, and it bit me: **CUDA 13 dropped Maxwell**, so the prebuilt binary refused to run and the host had no toolkit to rebuild. The fix was to build inside a `nvidia/cuda:12.5.1-devel` Docker container (CUDA 12.x still supports `sm_50`) with `-DCMAKE_CUDA_ARCHITECTURES=50`. With the NVIDIA Container Toolkit, `--gpus all` exposes the card and it Just Works — but CUDA's comfort comes with a leash.

**Verdict:** Best ergonomics and tooling, as long as you're on NVIDIA and your card is still supported.

## Vulkan — the most work, and it won

Vulkan was the most code by far (~760 lines of host glue plus GLSL compute shaders compiled to SPIR-V): devices, queues, command buffers, descriptor sets, pipelines, push constants, barriers — nothing implicit. That explicitness paid off: it was the fastest backend, with the shader tiling the *O(N²)* loop via push constants and using Kahan compensated summation for stability. The shader language is separate from your C++ and compiled offline — a cleaner model than runtime string compilation, but a context-switch between two languages.

**Verdict:** Steepest curve, most boilerplate, most portable, best control and speed. Overkill for a one-off kernel; ideal if compute lives inside a larger Vulkan renderer.

## OpenCL — portable in theory, footguns in practice

OpenCL genuinely saw both an NVIDIA and an Intel platform on this box. Kernels are C99-ish, compiled from source strings *at runtime* — flexible, but it pushes compile errors to runtime and adds device-selection boilerplate. Its sharpest footgun: the backend defaults to CPU and only uses the GPU with `--gpu`. Without that flag it silently ran the *O(N²)* pass on the CPU — **11 minutes** instead of 11 seconds, with no error.

**Verdict:** Unmatched breadth (NVIDIA, AMD, Intel, CPUs) at the cost of verbosity, runtime kernel compilation, and device-selection foot-guns.

## OpenGL compute — the "already have a context" option

GLSL compute shaders are the lowest-friction GPU compute *if you already have an OpenGL context* — no separate runtime, dispatched with `glDispatchCompute`. The compute-shader variant (~500 lines) landed third at 8.9 s. Downsides: you need a GL context (a window-system dependency even offscreen), the compute model is less expressive, and SSBO buffer management feels bolted-on. The plain-OpenGL variant was the slowest GPU backend.

**Verdict:** Great if compute is a small part of an existing OpenGL app; not where you'd start for a compute-first project.

## So which should you reach for?

- **All-in on NVIDIA, want results today?** CUDA — just mind the architecture/toolkit lifecycle (keep a Docker image handy for old cards).
- **Cross-vendor renderer with compute in the same stack?** Vulkan — lots of ceremony, most power and portability, fastest here.
- **Must run on anything, including non-NVIDIA and CPUs?** OpenCL — be explicit about device selection.
- **Already have an OpenGL app needing a compute pass?** OpenGL compute shaders.

The deeper lesson: on a well-suited, compute-bound workload, **the API barely affects throughput** — every one saturated the GPU and collapsed an 11-minute CPU job into seconds. What differs is the *engineering experience*: boilerplate, kernel language, portability, and how badly the toolchain can surprise you. Pick for the experience and ecosystem; the FLOPs show up regardless.

## Code

* <https://github.com/vladiant/color2gray>

---

*Benchmarks: 512×512 Lena.bmp, identical parameters, GTX 750 Ti (driver 580), single run. Time is the program's in-process timer; memory is peak host RSS; GPU util. via `nvidia-smi`. CUDA built/run in a `nvidia/cuda:12.5.1-devel` container.*
