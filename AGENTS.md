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

`index.html` shows exactly 8 featured projects. When updating the list, select by:

1. **Production-style architecture** — layered design, real databases, observability (metrics/traces/logs)
2. **Active maintenance** — recent commits, Dependabot, CI passing
3. **External validation** — stars, forks, or live deployments
4. **Breadth signal** — collectively cover: backend services, C++ systems, CV/GPU, quality engineering, polyglot CI

Current featured 8 and why each was chosen:

| Project | Repo | Signal |
|---|---|---|
| CommerceSystemDemo | vlantonov/CommerceSystemDemo | Production backend, OTel stack, live on Render |
| ImageProcessingServiceDemo | vlantonov/ImageProcessingServiceDemo | Cloud-native, Kafka, Kubernetes, Clean Architecture |
| CppConcurrencyPatterns | vladiant/CppConcurrencyPatterns | 25 stars, 2 forks — highest community validation |
| CascadeClassifier | vladiant/CascadeClassifier | Multi-platform CI, C++17, legacy modernization |
| color2gray | vladiant/color2gray | CUDA + OpenCL + Vulkan + OpenGL — GPU breadth |
| test_cpp_ci | vladiant/test_cpp_ci | Sanitizers, valgrind, static analysis template |
| test_golang_ci | vladiant/test_golang_ci | Go CI quality template, active Dependabot |
| test_java_ci | vladiant/test_java_ci | Java/Gradle CI template, JUnit Jupiter, active |

**Not featured** (demoted — tutorial-level scope): `grpc_samples`, `KafkaTutorial`.

### How to Update Featured Projects

1. Fetch the target repo's README/activity from GitHub to confirm: recency, CI status, depth
2. Edit the `.project-card` entries in `index.html` — each card must have: `<h3><a>`, `<p>` description (1–2 sentences), and `<div class="project-meta">` with 4 tech tags
3. Keep the 8-project cap. Replace weakest entry in the same thematic slot (backend / C++ systems / CV-GPU / quality-CI)
4. Run `bundle exec jekyll build` to verify before committing

## Nav & Footer (default.html)

- Nav: `.brand` (left) + `<ul>` links (right) via `margin-left: auto`
- Footer: `.footer-inner` with `.footer-links` (flex, centered) + `.footer-copy`
- Both are in `_layouts/default.html` and apply to all pages

## Common Pitfalls

- **Gems**: Never install gems system-wide; always use `vendor/bundle` (already configured)
- **CSS variables**: Declare in `:root {}` and reference with `var(--name)` — do not hardcode colors
- **`nav.site-nav ul`** has two rule blocks — the second one (`display: flex; gap: 22px; ...`) is the canonical one; the first sets `margin-left: auto` only
- **Responsive nav**: at ≤900px the `.nav-inner` stacks vertically (`flex-direction: column`)
