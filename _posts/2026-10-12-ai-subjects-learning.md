---
layout: post
title: "AI Subjects Learning"
date: 2026-10-12    
tags: design ai coding
---

## AI Proficiency Requirements

* Proficient integrating AI coding assistants, CLIs, and MCPs into daily development workflows.
* Uses AI effectively across the SDLC - planning, design, implementation, debugging, deployment, and observability.
* Builds reusable AI tooling (agent rules, skills, internal MCPs) that compounds team productivity, with sound judgment on when AI is (and isn't) the right tool.
* Balances AI-driven velocity with engineering rigor - automated testing, structural guardrails, and CI checks to validate AI-generated code.

## 1. AI coding assistants, CLIs & MCP in daily workflows

* [Anthropic - Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices) - the canonical field guide for CLI-driven agentic coding: CLAUDE.md conventions, workflow patterns, multi-agent orchestration.
* [Claude Code Docs - Best Practices](https://code.claude.com/docs/en/best-practices) - living doc, updated frequently; covers plugins, skills/subagents/hooks/MCP decision-making, and codebase-onboarding patterns.
* [Anthropic - Writing effective tools for AI agents](https://www.anthropic.com/engineering/writing-tools-for-agents) - how tool/MCP description quality directly affects agent reliability (SWE-bench data included).
* [DeepLearning.AI - MCP: Build Rich-Context AI Apps with Anthropic](https://www.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic) - free, ~2 hrs, taught by Anthropic's head of technical education; builds a real MCP server/client end to end (FastMCP, resources, prompts, remote deployment).
* [Simon Willison - MCP tag archive](https://simonwillison.net/tags/model-context-protocol/) and his [Agentic Engineering Patterns](https://simonw.substack.com/p/agentic-engineering-patterns) - practitioner notes on what actually works day-to-day, including where MCP helps vs. where plain CLIs/libraries beat it.
* [Firecrawl - 10 Best MCP Servers for Developers in 2026](https://www.firecrawl.dev/blog/best-mcp-servers-for-developers) - practical map of which MCP servers are worth wiring into a real workflow right now.

## 2. AI across the full SDLC (plan → design → implement → debug → deploy → observe)

* [Martin Fowler - martinfowler.com AI-assisted programming articles](https://martinfowler.com/) (search "AI" tag) - his pieces on LLM-augmented programming, spec-driven development, and "on the loop" human roles are the most rigorous non-vendor writing on this.
* [Kief Morris / Martin Fowler - Where Do Humans Fit in AI-Assisted Software Development](https://infoq.com/news/2026/03/mf-aiassisted-dev) (InfoQ summary) - on shifting from reviewing every artifact to designing specs/tests/feedback loops that govern agents.
* [Google Cloud DORA - Balancing AI tensions: Moving from AI adoption to effective SDLC use](https://dora.dev/insights/balancing-ai-tensions/) and the [2025 DORA State of AI-assisted Software Development report](https://dora.dev/ai/) - the best evidence-based look at where AI speeds up the SDLC and where it just relocates the bottleneck ("verification tax").
* [The New Stack - Martin Fowler on Preparing for AI's Nondeterministic Computing](https://thenewstack.io/martin-fowler-on-preparing-for-ais-nondeterministic-computing/) - his "treat every AI diff like a PR from a productive but untrustworthy collaborator" framing, plus tolerance/structural-engineering analogy for judging AI fit.

## 3. Reusable AI tooling - agent rules, skills, internal MCPs, and judgment on when to use AI

Given what's already in your Copilot agent infrastructure work, these map directly onto it:

* [Anthropic - Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) - the foundational explainer: skills as folders (not just markdown), when code beats tokens, how discovery works.
* [Anthropic - Lessons from building Claude Code: How we use skills](https://claude.com/blog/lessons-from-building-claude-code-how-we-use-skills) - internal Anthropic playbook: only write skills for things that push the model off its defaults, "Gotchas" sections as highest-signal content, iterate from real failures.
* [Anthropic - Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) - the widely-cited framework for choosing workflows vs. autonomous agents, and when *not* to reach for agentic complexity - directly useful for your "sound judgment on when AI is/isn't the right tool" goal.
* shanraisshan/claude-code-best-practice GitHub repo (referenced in the [mcp.directory writeup](https://mcp.directory/blog/claude-code-best-practices)) - community-maintained, heavily-starred consolidation of commands/agents/skills/hooks/MCP patterns.

## 4. Balancing AI velocity with engineering rigor (testing, guardrails, CI)

* [minware - Why the Test Pyramid Matters More Than Ever in AI-Assisted Development](https://www.minware.com/blog/test-pyramid-ai-assisted-development) - concrete argument for fast local checks as the safety net against AI-inflated PR size and defect rate.
* Martin Fowler's site - pieces on using test suites as regression sensors for AI agents, and static-analysis "maintainability sensors" (linting, dependency rules, coupling) to keep AI-touched codebases clean - both referenced in the [AllDevBlogs Fowler roundup](https://www.alldevblogs.com/blog/martin-fowler).
* [DORA - ROI of AI-assisted Software Development report](https://dora.dev/ai/) - introduces the "verification tax" and J-curve model; useful for arguing to a team/manager why review and CI investment must scale alongside AI adoption, not lag behind it.
* [InfoQ - New DORA Report: Strong Engineering Foundations Drive AI ROI](https://www.infoq.com/news/2026/05/dora-roi-ai-assisted-dev-report/) - summary of why platform quality and workflow clarity (not tool choice) determine whether AI velocity gains survive contact with production.

## Video talks (all free)

### AI assistants, CLIs & MCP in daily workflow
* [Simon Willison - Engineering practices that make coding agents work](https://www.youtube.com/watch?v=owmJyKVu5f8) (The Pragmatic Summit, ~30 min, Feb 2026) - fireside chat covering red-green TDD with agents, his "Showboat" manual-testing tool, the lethal-trifecta security framework, and which model he actually trusts for professional work. Companion write-up with extra notes: [simonwillison.net/2026/Mar/14/pragmatic-summit](https://simonwillison.net/2026/Mar/14/pragmatic-summit/).
* [Agent Skills or MCP in the era of Claude Code?](https://www.youtube.com/watch?v=pvxNcQTcIy4) - Tim Berglund (Confluent/DevRel veteran) lightboard explainer on how Skills changes the calculus for when you reach for MCP vs. skills vs. plain tool use.
* [AWS re:Invent 2025 - Accelerate multi-step SDLC with Kiro (DVT321)](https://dev.to/kazuya_dev/aws-reinvent-2025-accelerate-multi-step-sdlc-with-kiro-dvt321-5h2d) - live demo building an app end-to-end with a custom agent config using the "AI-DLC" methodology; useful even if you don't use Kiro, since the phase breakdown (spec → design → tasks → build) generalizes to any CLI agent.

### AI across the full SDLC
* [The New SDLC: From Vibe Coding to Agentic Engineering](https://www.youtube.com/watch?v=Z5IyvfWwams) (Google × Kaggle AI Agents Intensive) - walks through how AI touches each SDLC phase differently, with a clear framing of what changes at planning vs. implementation vs. review stages.
* [GitHub Universe 2025 Announcements + Reactions](https://www.youtube.com/watch?v=sblq5THb1no) - GitHub staff reacting live to Agent HQ, Copilot's move into planning/orchestration/review, and the shift toward what GitHub calls the "agentic development lifecycle." Good for seeing where platform vendors are pushing observability and control planes.

### Reusable AI tooling & judgment on when to use it
* [Máster Claude Code 2026: Agentes IA, MCP, Skills y Comandos](https://www.youtube.com/watch?v=roPfcQHdUtY) (Spanish) - long-form, hands-on walkthrough of building custom agents, skills, and slash commands; skip if you need English, but it's one of the more thorough free build-alongs if Spanish works for you.

### Balancing velocity with engineering rigor
- Most of the good material here (Fowler, DORA, minware) is written, not recorded. If a talk surfaces later, the QCon AI Boston 2026 session ["Prompt to Prod: Engineering an Autonomous SDLC at Scale"](https://boston.qcon.ai/presentation/boston2026/prompt-prod-engineering-autonomous-sdlc-scale) (Roblox's engineering-acceleration lead, on agentic guardrails and self-healing codebases) may get a recording posted post-event - worth checking QCon's YouTube channel.
