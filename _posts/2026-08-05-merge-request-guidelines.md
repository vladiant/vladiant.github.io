---
layout: post
title: "Merge Request Description Guidelines"
date: 2026-08-05    
tags: development ai
---

## Guidelines for Pull/Merge Request Descriptions — Portfolio Projects

These guidelines are meant for changes to public, portfolio-style software repositories (demo apps, reference implementations, libraries) where the audience for a PR/MR description is broader than a single internal team: future employers, collaborators discovering the repo, and future-you returning to the project months later.

### 1. Title

- One line, imperative mood, complete sentence in spirit (no trailing period): `Add object pool benchmark for small allocations`, not `Added stuff` or `Fixes`.
- State *what* changed, not *how* internally — save mechanism details for the body.
- If the project uses Conventional Commits, prefix with a type/scope for consistency with commit history and changelog tooling: `feat(pool): add benchmark for small allocations`.
- Keep it under ~70 characters so it doesn't truncate in PR lists or commit-log views.

### 2. Summary (first paragraph)

- 2–4 sentences answering: what problem does this solve, and why does it matter for this project?
- Written for someone with zero context on the current branch — assume they haven't read the diff yet.
- For a portfolio repo, this is also the paragraph a reviewer or recruiter skims first, so lead with the value, not the implementation detail.

### 3. Motivation / context

- Why is this change needed now? Link the originating issue, TODO checklist item, or design doc if one exists.
- If this closes or relates to a tracked task (e.g. a portfolio-improvement checklist item), reference it explicitly: `Closes #12` or `Addresses item P1-3 in portfolio-todo.md`.
- Mention any shortcomings or known limitations of the chosen approach up front — don't let a reviewer discover them.

### 4. What changed

- A short bulleted list of the concrete changes, grouped logically (not a raw file list — the diff already shows that).
- Call out anything non-obvious: new build targets, changed CMake options, new third-party dependencies, ABI/API breaks.
- For portfolio/demo repos specifically, note any change that affects how someone else would clone-and-run the project (new prerequisites, changed entry point, new environment variable).

### 5. How it was tested / verified

- State what was actually run: unit tests (GoogleTest/Catch2), sanitizers (ASan/UBSan/TSan), static analysis, manual run-through, benchmark comparisons.
- Include before/after numbers for anything performance-related — a single sentence with old vs. new is far more convincing than "improved performance."
- If something intentionally isn't covered by tests yet, say so rather than implying full coverage.

### 6. Screenshots / output samples (if applicable)

- For anything with visible output (image-processing demos, CLI tools, dashboards), include a before/after screenshot or console excerpt. This carries a lot of weight for a portfolio audience skimming quickly.

### 7. Checklist (optional but recommended for portfolio repos)

A short checklist at the end signals rigor to anyone evaluating the repo:
- [ ] Builds cleanly with the project's CMake presets
- [ ] Tests pass locally
- [ ] Documentation / README updated if behavior or usage changed
- [ ] No new compiler warnings introduced

### 8. General style notes

- Prefer prose + bullets over a wall of text; reviewers and future readers skim.
- Write the description before starting the review request, not as an afterthought — treat it as documentation, since for a portfolio project the PR history often *is* the design record.
- Keep unrelated changes out of the same PR; a focused PR gets a focused, useful description almost for free.
- If you deliberately deviate from an established pattern in the repo (e.g. an SDLC agent convention or existing architectural style), say why.

---

### Notes

* Google's engineering-practices guidance recommends that the first line of a change description be a short, complete-sentence imperative summary that stands alone in version-control history, followed by a body that explains the problem being solved and why the chosen approach is appropriate, including any shortcomings and links to relevant background such as bug numbers or benchmark results.

* The Conventional Commits specification is a lightweight, structured convention for commit messages — pairing a type and optional scope with a description — that supports automated changelog generation and semantic-version bumps.

* GitHub's own guidance for pull requests emphasizes keeping PRs small and focused on a single purpose, since smaller PRs are easier and faster to review, reduce the chance of introduced bugs, and leave a clearer history of changes. It also frames pull requests as more than a code diff — they're a way to keep collaborators informed and to connect work back to the relevant issues or project tracking.

* GitHub's internal guidelines for writing pull requests recommend stating the purpose of the PR plainly and providing an overview of why the change is needed.

### References:
- Google Engineering Practices — "Writing Good CL Descriptions": <https://google.github.io/eng-practices/review/developer/cl-descriptions.html>
- Conventional Commits specification (v1.0.0): <https://www.conventionalcommits.org/en/v1.0.0/>
- GitHub Docs — "Helping others review your changes" / best practices for pull requests: <https://docs.github.com/en/enterprise-server@3.12/pull-requests/collaborating-with-pull-requests/getting-started/best-practices-for-pull-requests>
- GitHub Blog — "How to write the perfect pull request": <https://github.blog/developer-skills/github/how-to-write-the-perfect-pull-request/>


