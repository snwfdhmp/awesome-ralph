
<p align="center">
  <a href="https://www.reddit.com/r/RalphCoding/">
<img src="https://github.com/user-attachments/assets/692be4b4-8bd9-4002-af29-9e65c5e6b61c" width="1000" alt="Ralph Wiggum AI Coding method">
  </a>
</p>


# Awesome Ralph [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![Follow on X](https://img.shields.io/twitter/follow/snwfdhmp?style=social)](https://x.com/snwfdhmp)

> A curated list of resources about Ralph (aka Ralph Wiggum), the AI coding technique that runs AI coding agents in automated loops until specifications are fulfilled.

Ralph is a technique created by [Geoffrey Huntley](https://ghuntley.com) for autonomous AI coding. The core concept is elegantly simple:

```bash
while :; do cat PROMPT.md | claude-code ; done
```

**Key principles:**
- Run an AI agent repeatedly until a PRD/specification is complete
- Progress persists in files and git history, not in context
- Each iteration starts fresh with clean context
- Use "backpressure" (tests, lints, type checks) to validate work
- Philosophy: *"Sit on the loop, not in it"* — or as Huntley puts it: *"deterministically bad in an undeterministic world"*

> **Found this useful? ⭐️ Like this repo to help others discover it**

## Contents

- [Official Resources](#official-resources)
- [Playbooks & Methodology](#playbooks--methodology)
- [Implementations](#implementations)
  - [Claude Code Plugins](#claude-code-plugins)
  - [Standalone Implementations](#standalone-implementations)
  - [Tool-Specific Implementations](#tool-specific-implementations)
  - [Multi-Agent Systems](#multi-agent-systems)
- [Tutorials & Guides](#tutorials--guides)
- [Articles & Blog Posts](#articles--blog-posts)
- [Videos & Podcasts](#videos--podcasts)
  - [Videos](#videos)
  - [Podcasts](#podcasts)
- [Community](#community)
  - [Hacker News Discussions](#hacker-news-discussions)
  - [Tools & Directories](#tools--directories)
  - [Ralph Communities](#ralph-communities)
- [Related Tools](#related-tools)
- [Support](#support)
- [Contributing](#contributing)

## Official Resources

Primary sources from Geoffrey Huntley, the creator of the Ralph technique.

- [Ralph Wiggum as a 'Software Engineer'](https://ghuntley.com/ralph/) - The definitive introduction. Explains the bash loop, "tuning like a guitar" metaphor, and the economics of autonomous coding.
- [Everything is a Ralph Loop](https://ghuntley.com/loop/) - Deeper philosophical exploration covering "reverse mode" clean-rooming, orchestrator patterns, and "The Weaving Loom" concept.
- [Don't Waste Your Back Pressure](https://ghuntley.com/pressure/) - Technical deep-dive on backpressure — the art of rejecting invalid generations without creating too much resistance.
- [I Ran Claude in a Loop for Three Months](https://ghuntley.com/cursed/) - Case study: Ralph built CURSED, a Gen Z slang-based programming language with LLVM compiler.
- [Too Many Model Context Protocol Servers](https://ghuntley.com/allocations/) - Context allocation theory — Ralph minimizes allocation to avoid compaction events.

## Playbooks & Methodology

Comprehensive implementation guides covering the **3 Phases, 2 Prompts, 1 Loop** workflow.

- [How to Ralph Wiggum](https://github.com/ghuntley/how-to-ralph-wiggum) - Geoffrey Huntley's official playbook covering context management, sandboxing, and prompt patterns.
- [ralph-playbook](https://github.com/ClaytonFarr/ralph-playbook) - Comprehensive methodology guide with diagrams, phase explanations, and "signs & gates" steering techniques.

### The Core Workflow

**Phase 1: Define Requirements** — Human + LLM conversation produces JTBD-aligned specifications
**Phase 2: Planning Mode** — Gap analysis generates prioritized TODO list (no implementation)
**Phase 3: Building Mode** — Implement from plan, run tests, commit, repeat

### Essential File Structure

```
project-root/
├── loop.sh                    # Ralph loop script
├── PROMPT_build.md            # Build mode instructions
├── PROMPT_plan.md             # Plan mode instructions
├── AGENTS.md                  # Operational guide (~60 lines max)
├── IMPLEMENTATION_PLAN.md     # Prioritized task list (generated)
├── specs/                     # Requirement specs (one per JTBD)
└── src/                       # Application source code
```

## Implementations

### Claude Code Plugins

- [ralph-claude-code](https://github.com/frankbria/ralph-claude-code) - Claude Code with intelligent exit detection, rate limiting, circuit breaker, and semantic response analyzer.
- [choo-choo-ralph](https://github.com/mj-meyer/choo-choo-ralph) - Beads-powered 5-phase workflow with structured specs, verified implementations, and compounding knowledge—per-project installation with fully customizable workflows.

### Standalone Implementations

- [snartank/ralph](https://github.com/snarktank/ralph) - PRD-driven task management with automatic branching, flowchart visualization, and auto-archiving.
- [iannuttall/ralph](https://github.com/iannuttall/ralph) - Minimal file-based agent loop supporting codex/claude/droid/opencode.
- [smart-ralph](https://github.com/tzachbon/smart-ralph) - Spec-driven development workflow. Transforms feature requests into structured specs (research, requirements, design, tasks) then executes them task-by-task autonomously.
- [ralph-wiggum-bdd](https://github.com/marcindulak/ralph-wiggum-bdd) - A standalone Bash script for Behavior-Driven Development with Ralph Wiggum Loop.
- [ralph-orchestrator](https://github.com/mikeyobrien/ralph-orchestrator) - Rust orchestrator with 7 AI backends, Hat System for specialized personas, and interactive TUI mode.
- [nitodeco/ralph](https://github.com/nitodeco/ralph) - CLI orchestration tool for PRD-driven development with sequential task execution and interactive terminal UI.
- [oh-my-ralph](https://github.com/vivganes/oh-my-ralph) - Opinionated Ralph Wiggum loop implemented in Python, available in [PyPI](https://pypi.org/search/?q=oh-my-ralph).

### Tool-Specific Implementations

- [ralph-wiggum-cursor](https://github.com/agrimsingh/ralph-wiggum-cursor) - Cursor implementation with token tracking, context rotation at 80k tokens, and interactive setup.
- [opencode-ralph-wiggum](https://github.com/Th0rgal/opencode-ralph-wiggum) - OpenCode implementation with real-time status display, mid-loop context injection, and struggle detection.
- [ralph (GitHub Copilot)](https://github.com/aymenfurter/ralph) - VS Code extension with visual Control Panel, Progress Timeline, and Fresh Chat Mode.
- [ralph-tui](https://github.com/subsy/ralph-tui) - Terminal UI orchestrator connecting to task trackers with interactive PRD creation.
- [Goose Ralph Loop Tutorial](https://block.github.io/goose/docs/tutorials/ralph-loop/) - Block's Goose implementation with cross-model review and recipe-based workflows.

### Multi-Agent Systems

- [ralph-loop-agent](https://github.com/vercel-labs/ralph-loop-agent) - Vercel's TypeScript SDK wrapper with verification callbacks and context summarization.
- [multi-agent-ralph-loop](https://github.com/alfredolopez80/multi-agent-ralph-loop) - Multi-agent orchestration for complex projects requiring parallel work streams.

## Tutorials & Guides

- [Getting Started with Ralph](https://www.aihero.dev/getting-started-with-ralph) - Step-by-step quickstart with Claude Code + Docker by Matt Pocock.
- [11 Tips for AI Coding with Ralph Wiggum](https://www.aihero.dev/tips-for-ai-coding-with-ralph-wiggum) - AFK coding, HITL Ralph, iteration caps, and progress tracking.
- [The Ralph Wiggum Approach](https://dev.to/sivarampg/the-ralph-wiggum-approach-running-ai-coding-agents-for-hours-not-minutes-57c1) - Stop hook mechanism, troubleshooting, and Q&A.
- [The Real Ralph Wiggum Loop](https://thetrav.substack.com/p/the-real-ralph-wiggum-loop-what-everyone) - Clarifies original bash loop vs Anthropic plugin philosophy.
- [Ralph Wiggum Guide](https://github.com/JeredBlu/guides/blob/main/Ralph_Wiggum_Guide.md) - Community-written comprehensive guide.
- [Awesome Claude - Ralph Wiggum](https://awesomeclaude.ai/ralph-wiggum) - Resource page with additional tips and configuration examples.
- [How to Build an Effective Long Running Agent Loop in 7 minutes.](https://x.com/dabit3/status/2013091003104727338?s=20) - Walks you through the entire process from creating a spec, building and polishing a PRD, to running the agent with frameworks like Claude Code, Codex, and OpenCode.

## Articles & Blog Posts

- [How Ralph Wiggum Went from The Simpsons to the Biggest Name in AI](https://venturebeat.com/technology/how-ralph-wiggum-went-from-the-simpsons-to-the-biggest-name-in-ai-right-now) - VentureBeat coverage on the cultural phenomenon.
- [A Brief History of Ralph](https://www.humanlayer.dev/blog/brief-history-of-ralph) - Comprehensive timeline including Y Combinator hackathon story.
- [Ralph Wiggum and AI Coding Loops](https://www.ishir.com/blog/312751/ralph-wiggum-and-ai-coding-loops-from-springfield-to-real-world-software-automation.htm) - From Springfield to real-world software automation.
- [Ralph Wiggum Explained: The Claude Code Loop That Keeps Going](https://blog.devgenius.io/ralph-wiggum-explained-the-claude-code-loop-that-keeps-going-3250dcc30809) - Technical explainer of how and why it works.
- [2026: The Year of the Ralph Loop Agent](https://dev.to/alexandergekov/2026-the-year-of-the-ralph-loop-agent-1gkj) - Predictions and analysis of the Ralph loop's impact on development.

## Videos & Podcasts

### Videos

- [Ralph Wiggum Deep Dive with Geoffrey Huntley](https://www.youtube.com/watch?v=SB6cO97tfiY) - The definitive video. Live coding demo, history, and comparison of bash-loop vs stop-hook implementations.
- [AI That Works Podcast Episode](https://www.youtube.com/watch?v=fOPvAPdqgPo) - 75-minute deep dive on why Ralph works — context windows, control loops, and applications.
- [Matt Pocock's Ralph Overview](https://www.youtube.com/watch?v=_IK18goX4X8) - Popular practical overview grounded in kanban and requirements discovery.

### Podcasts

- [Inventing the Ralph Wiggum Loop - Dev Interrupted](https://linearb.io/dev-interrupted/podcast/inventing-the-ralph-wiggum-loop) - Geoffrey Huntley on context rot, compaction, and the $10.42/hour calculation.
- [Inventing the Ralph Wiggum Loop (Transcript)](https://devinterrupted.substack.com/p/inventing-the-ralph-wiggum-loop-creator) - Full transcript of the Dev Interrupted episode.
- [Ralph Wiggum Coding Agent Power Tools - BoundaryML](https://boundaryml.com/podcast/2025-10-28-ralph-wiggum-coding-agent-power-tools) - Deep dive into tooling and advanced techniques.
- [Ralph Wiggum AI Agent Explained - Startup Ideas Podcast](https://www.podscan.fm/podcasts/the-startup-ideas-podcast/episodes/ralph-wiggum-ai-agent-explained-amp-how-to-use-it) - Accessible introduction for founders and builders.

## Community

### Hacker News Discussions

- [We Put a Coding Agent in a While Loop](https://news.ycombinator.com/item?id=45005434) - Geoffrey Huntley participated; security concerns raised about default passwords.
- [Ralph Wiggum as a Software Engineer](https://news.ycombinator.com/item?id=43817200) - Code quality critiques and maintainability debates.
- [Original HN Discussion](https://news.ycombinator.com/item?id=44565028) - The discussion that helped popularize the technique.
- [Tips Discussion](https://news.ycombinator.com/item?id=46547129) - Community tips and experiences thread.
- [Ralph from First Principles (Video)](https://news.ycombinator.com/item?id=46587275) - Discussion around educational video content.
- [What Happens After Ralph Wiggum?](https://news.ycombinator.com/item?id=46632445) - Exploring the future of autonomous coding patterns.

### Tools & Directories

- [Vibe Coding - Ralph Wiggum Loop](https://vibecoding.app/tools/ralph-wiggum-loop) - Tool directory entry with quick-start resources.

### Ralph Communities

- [r/ralphcoding](https://www.reddit.com/r/RalphCoding/) - A subreddit about Ralph Coding. Share your learnings, resources, achievements with the community.
- [Ralph Discord](https://discord.gg/MUyRMqKcWx) - Discord community discussing Ralph methods/resources/achievements.

## Related Tools

- [Advanced Context Engineering for Coding Agents](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents) - Techniques for optimizing context windows and prompts for autonomous agents.

## Support

If this list helped you discover useful Ralph resources, please give it a ⭐️ star! It helps others find this collection.

[![Stargazers repo roster for @snwfdhmp/awesome-ralph](https://reporoster.com/stars/snwfdhmp/awesome-ralph)](https://github.com/snwfdhmp/awesome-ralph/stargazers)

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

Join the community on [Discord](https://discord.gg/MUyRMqKcWx) and [Reddit](https://www.reddit.com/r/RalphCoding/)
