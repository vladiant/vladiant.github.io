# Agent Instructions — vladiant.github.io

Jekyll-based personal portfolio and technical blog for Vladislav Antonov (Senior C++ Developer & Software Architect).

## Build & Serve

```bash
# Install gems (first time only — local vendor/ avoids sudo)
bundle config set --local path vendor/bundle
bundle install

# Build
bundle exec jekyll build

# Serve locally (port 4001)
bundle exec jekyll serve --host 127.0.0.1 --port 4001
```

Build succeeds with exit 0. The only expected warning is:
`Build Warning: Layout 'feed' requested in blog/atom.xml does not exist.` — this is pre-existing and benign.

## Architecture

| File/Dir | Purpose |
|---|---|
| `index.html` | Homepage — featured projects and hero section |
| `_layouts/default.html` | Shared nav + footer shell for all pages |
| `css/main.css` | All styling — dark theme, CSS variables, responsive |
| `_posts/` | Blog posts in Markdown (`YYYY-MM-DD-slug.md`) |
| `about/index.html` | About page |
| `_includes/` | Partials: analytics, tag helpers |
| `_config.yml` | Jekyll site config |

## Design System (css/main.css)

CSS variable reference:
- `--bg: #0d1117` · `--surface: #161b22` · `--border: #30363d`
- `--text: #c9d1d9` · `--text-dim: #8b949e` · `--text-bright: #f0f3f6`
- `--amber: #e8a23d` (primary accent/links) · `--signal: #3fb98c` (secondary accent)
- `--mono: 'IBM Plex Mono'` · `--sans: 'Inter'`

Breakpoints: 900px (tablet), 600px (mobile). Max content width: 920px via `.wrap`.

## Featured Projects — Selection Criteria

`index.html` shows exactly 8 featured projects. The page brands a **Senior C++ Developer & Software Architect**, so the showcase must lead with *architecture and depth*, not hygiene or language count. Candidates are drawn from three profiles: [github.com/vladiant](https://github.com/vladiant) (C++/CV/GPU), [github.com/vlantonov](https://github.com/vlantonov) (backend/service systems), and unique projects on [gitlab.com/vladiant](https://gitlab.com/vladiant). Select by, in priority order:

1. **Substantive system or deep library (primary gate)** — layered architecture, domain modeling, real data stores, or a non-trivial algorithm/library. Scaffolding, CI templates, and tutorial-scope repos do **not** clear this gate on their own.
2. **Engineering depth & judgment** — TDD/acceptance suites, quality gates (sanitizers, warnings-as-errors, static analysis, valgrind), documented design decisions, spec-driven or clean-architecture structure.
3. **Production / operational signal** — live deployment, full observability (metrics/traces/logs), containerization or orchestration. A live deployment outweighs star count.
4. **External validation (secondary)** — stars, forks, and active maintenance (recent commits, Dependabot, CI passing). Useful as a tie-breaker, never as the main reason to feature.
5. **Breadth guard** — the 8 must collectively span: backend/distributed systems, C++ systems, CV/GPU, and quality engineering. Cap CI-template / scaffolding repos at **one** slot so depth is not crowded out by near-identical boilerplate.

Current featured 8 and why each was chosen (thematic slot in brackets):

| Project | Repo | Signal |
|---|---|---|
| CommerceSystemDemo | vlantonov/CommerceSystemDemo | [backend] Production backend, async PostgreSQL, full OTel stack, live on Render |
| ImageProcessingServiceDemo | vlantonov/ImageProcessingServiceDemo | [backend] Cloud-native, Kafka, Kubernetes, Clean Architecture |
| SimpleBankingTaskDemo | vlantonov/SimpleBankingTaskDemo | [C++ systems] Layered C++ ATM service, HTTP adapter, acceptance/BDD TDD, actively developed |
| MobileNetworkOperatorDemo | vlantonov/MobileNetworkOperatorDemo | [C++ systems] C++17 billing engine, spec-driven design, warnings-as-errors + ctest quality gates |
| CppConcurrencyPatterns | vladiant/CppConcurrencyPatterns | [C++ systems] 25 stars, 2 forks — highest community validation |
| color2gray | vladiant/color2gray | [CV/GPU] CUDA + OpenCL + Vulkan + OpenGL — GPU compute breadth |
| CascadeClassifier | vladiant/CascadeClassifier | [CV/GPU] Multi-platform CI, C++17, legacy OpenCV modernization |
| test_cpp_ci | vladiant/test_cpp_ci | [quality] Sanitizers, valgrind, static analysis — the single allowed CI-template slot |

**Not featured** (demoted — scaffolding/tutorial-level scope, crowd out depth): `test_golang_ci`, `test_java_ci`, `test_python_ci`, `grpc_samples`, `KafkaTutorial`. The Go/Java/Python CI templates remain strong hygiene artifacts but are represented by the single `test_cpp_ci` slot per the breadth guard.

### How to Update Featured Projects

1. Fetch the target repo's README/activity (GitHub `vladiant`/`vlantonov` or GitLab `vladiant`) to confirm: depth (system vs. scaffolding), engineering signals, recency, CI status, deployment
2. Confirm the candidate clears criterion 1 (substantive system/library) before anything else — do not feature scaffolding to fill a language gap
3. Edit the `.project-card` entries in `index.html` — each card must have: `<h3><a>`, `<p>` description (1–2 sentences), and `<div class="project-meta">` with 4 tech tags
4. Keep the 8-project cap and the thematic balance (≥2 backend/distributed, ≥3 C++ systems, ≥2 CV/GPU, exactly 1 quality/CI). Replace the weakest entry in the same slot
5. Run `bundle exec jekyll build` to verify before committing

## Nav & Footer (default.html)

- Nav: `.brand` (left) + `<ul>` links (right) via `margin-left: auto`
- Footer: `.footer-inner` with `.footer-links` (flex, centered) + `.footer-copy`
- Both are in `_layouts/default.html` and apply to all pages

## Common Pitfalls

- **Gems**: Never install gems system-wide; always use `vendor/bundle` (already configured)
- **CSS variables**: Declare in `:root {}` and reference with `var(--name)` — do not hardcode colors
- **`nav.site-nav ul`** has two rule blocks — the second one (`display: flex; gap: 22px; ...`) is the canonical one; the first sets `margin-left: auto` only
- **Responsive nav**: at ≤900px the `.nav-inner` stacks vertically (`flex-direction: column`)
