# Awesome Ralph [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![Follow on X](https://img.shields.io/twitter/follow/snwfdhmp?style=social)](https://x.com/snwfdhmp)

<a href="https://ghuntley.com"><img src="https://github.com/user-attachments/assets/692be4b4-8bd9-4002-af29-9e65c5e6b61c" width="1000" alt="Ralph Wiggum AI coding method"></a>

> Ralph (aka the Ralph Wiggum loop) is an AI coding technique that runs a coding agent in a loop, with fresh context on every iteration, until a specification is fulfilled.

Ralph was created by Geoffrey Huntley. The core concept is elegantly simple:

```bash
while :; do cat PROMPT.md | claude-code ; done
```

**Key principles:**

- Run an AI agent repeatedly until a PRD/specification is complete.
- Progress persists in files and Git history, not in context.
- Each iteration starts fresh with clean context.
- Use "backpressure" (tests, lints, type checks) to validate work.
- Philosophy: *"Sit on the loop, not in it"*, or as Huntley puts it: *"deterministically bad in an undeterministic world"*.

> **Found this useful? ⭐️ Star this repo to help others discover it.**

## Contents

- [Official Resources](#official-resources)
- [Playbooks and Methodology](#playbooks-and-methodology)
- [Implementations](#implementations)
  - [Official Plugins](#official-plugins)
  - [Claude Code Plugins](#claude-code-plugins)
  - [Standalone CLIs](#standalone-clis)
  - [Agent-Specific Implementations](#agent-specific-implementations)
  - [Orchestrators and Interfaces](#orchestrators-and-interfaces)
  - [SDKs and Libraries](#sdks-and-libraries)
  - [Beyond Coding](#beyond-coding)
- [Companion Tools](#companion-tools)
  - [Planning and Specs](#planning-and-specs)
  - [Loop Control and Guardrails](#loop-control-and-guardrails)
- [Vendor Guides](#vendor-guides)
- [Tutorials and Guides](#tutorials-and-guides)
- [Articles](#articles)
- [Case Studies](#case-studies)
- [Critiques](#critiques)
- [News](#news)
- [Videos](#videos)
- [Talks](#talks)
- [Podcasts](#podcasts)
- [Discussions](#discussions)
- [Communities](#communities)

## Official Resources

Primary sources from Geoffrey Huntley, the creator of the Ralph technique.

- [Ralph Wiggum as a 'Software Engineer'](https://ghuntley.com/ralph/) - The definitive introduction. Explains the bash loop, the "tuning like a guitar" metaphor, and the economics of autonomous coding.
- [Everything is a Ralph Loop](https://ghuntley.com/loop/) - Deeper exploration covering "reverse mode" clean-rooming, orchestrator patterns, and "The Weaving Loom" concept.
- [Don't Waste Your Back Pressure](https://ghuntley.com/pressure/) - Backpressure explained: rejecting invalid generations without creating too much resistance.
- [I Ran Claude in a Loop for Three Months](https://ghuntley.com/cursed/) - Case study: Ralph built CURSED, a Gen Z slang programming language with an LLVM compiler.
- [Too Many Model Context Protocol Servers](https://ghuntley.com/allocations/) - Context allocation theory, and why Ralph minimizes allocation to avoid compaction.
- [Porting Software Has Been Trivial for a While Now](https://ghuntley.com/porting/) - Two-stage Ralph recipe for porting: turn tests into specs, then run a TODO-driven loop.
- [Software Development Now Costs Less Than the Wage of a Minimum Wage Worker](https://ghuntley.com/real/) - Essay on the economic impact of running Ralph loops at scale.
- [The Eighteen-Month Recap](https://ghuntley.com/eighteen-month-recap/) - Talk write-up from AI Engineer Singapore revisiting Ralph and loop engineering.
- [If Your Team Is Too Busy to Learn, You're Preparing Them to Be Replaced](https://ghuntley.com/replaced/) - Reflection on Ralph going viral, with reader adoption stories.

## Playbooks and Methodology

Implementation guides covering the **3 Phases, 2 Prompts, 1 Loop** workflow.

- [How to Ralph Wiggum](https://github.com/ghuntley/how-to-ralph-wiggum) - Geoffrey Huntley's official playbook covering context management, sandboxing, and prompt patterns.
- [ralph-playbook](https://github.com/ClaytonFarr/ralph-playbook) - Methodology guide with diagrams, phase explanations, and "signs & gates" steering techniques.
- [Ralph Loop Prompts](https://github.com/invincible04/awesome-loop-engineering/blob/main/prompts/ralph-loops.md) - Annotated library of copy-paste Ralph prompts, each traced to its original author.
- [Advanced Context Engineering for Coding Agents](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents) - HumanLayer's Research-Plan-Implement approach to keeping agent context small.

### The Core Workflow

**Phase 1: Define requirements.** A human and an LLM converse to produce JTBD-aligned specifications.

**Phase 2: Plan.** Gap analysis generates a prioritized TODO list, with no implementation.

**Phase 3: Build.** Implement from the plan, run tests, commit, repeat.

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

### Official Plugins

- [Ralph Loop for Claude Code](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/ralph-loop) - Anthropic's plugin that uses a Stop hook to re-feed the prompt until a completion promise or iteration cap is reached. Formerly named `ralph-wiggum`.
- [Ralph Loop for Cursor](https://github.com/cursor/plugins/tree/main/ralph-loop) - Cursor's official port of the Stop-hook loop, built from hooks and skills.

### Claude Code Plugins

- [ralph-claude-code](https://github.com/frankbria/ralph-claude-code) - Claude Code loop with exit detection, rate limiting, a circuit breaker, and a response analyzer.
- [choo-choo-ralph](https://github.com/mj-meyer/choo-choo-ralph) - Beads-powered 5-phase workflow with structured specs, verified implementations, and compounding knowledge.
- [humanize](https://github.com/PolyArch/humanize) - Ralph loop with an independent Codex review step, built on the official Ralph Loop plugin.

### Standalone CLIs

Agent-agnostic loop runners.

- [snarktank/ralph](https://github.com/snarktank/ralph) - PRD-driven task loop with automatic branching, flowchart visualization, and auto-archiving.
- [ralphy](https://github.com/michaelshimeles/ralphy) - Bash loop that runs Claude Code, Codex, OpenCode, Cursor, Qwen, or Droid until a PRD is complete.
- [gnhf](https://github.com/kunchenguid/gnhf) - Overnight orchestrator where each iteration makes one small committed change.
- [open-ralph-wiggum](https://github.com/Th0rgal/open-ralph-wiggum) - `ralph "prompt"` CLI for OpenCode, Claude Code, Codex, and Copilot with live status, mid-loop context injection, and struggle detection.
- [ralphex](https://github.com/umputun/ralphex) - Go runner that executes a plan file task by task with Claude Code or Codex, adding plan creation and review stages.
- [continuous-claude](https://github.com/AnandChowdhary/continuous-claude) - Runs Claude Code in a loop that opens PRs, waits for CI, and merges.
- [ralph-orchestrator](https://github.com/mikeyobrien/ralph-orchestrator) - Rust orchestrator with 7 AI backends, a Hat System for specialized personas, and an interactive TUI.
- [chief](https://github.com/MiniCodeMonkey/chief) - Splits work into tasks and runs Claude Code in a fresh-context loop until they are done.
- [ralph-starter](https://github.com/rubenmarcus/ralph-starter) - CLI with GitHub, Linear, and Notion integrations, multiple agents, workflow presets, and cost tracking.
- [PageAI-Pro/ralph-loop](https://github.com/PageAI-Pro/ralph-loop) - npm-packaged long-running loop over a task list.
- [fstandhartinger/ralph-wiggum](https://github.com/fstandhartinger/ralph-wiggum) - Spec-driven Ralph setup distributed as an agent skill that the agent installs itself.
- [smart-ralph](https://github.com/tzachbon/smart-ralph) - Turns feature requests into research, requirements, design, and task specs, then executes them task by task.
- [loop.js](https://github.com/loop-js/loop.js) - Fresh-context loop with a separate read-only Verify agent that decides when to stop.
- [wreckit](https://github.com/mikehostetler/wreckit) - Spec-driven Ralph loop implementation.
- [SantanderAI/ralph](https://github.com/SantanderAI/ralph) - Configurable Bash and PowerShell loop that runs any AI coding CLI with a fresh session per iteration.
- [nitodeco/ralph](https://github.com/nitodeco/ralph) - PRD-driven CLI with sequential task execution and an interactive terminal UI.
- [oh-my-ralph](https://github.com/vivganes/oh-my-ralph) - Opinionated Ralph loop written in Python.
- [ralph-wiggum-bdd](https://github.com/marcindulak/ralph-wiggum-bdd) - Standalone Bash script for Behavior-Driven Development with a Ralph loop.
- [ralph-kit](https://github.com/develo-pera/ralph-kit) - Conversational project setup, a local Kanban dashboard, and a runner that works with other Ralph implementations.

### Agent-Specific Implementations

- [ralph-wiggum-cursor](https://github.com/agrimsingh/ralph-wiggum-cursor) - Cursor implementation with token tracking, context rotation at 80k tokens, and interactive setup.
- [CodexPotter](https://github.com/breezewish/CodexPotter) - Codex runner that keeps reconciling the codebase toward a stated goal using the Ralph pattern.
- [aymenfurter/ralph](https://github.com/aymenfurter/ralph) - VS Code extension for GitHub Copilot with a visual control panel, progress timeline, and fresh-chat mode.
- [ralph-copilot](https://github.com/giocaizzi/ralph-copilot) - Ralph loop for GitHub Copilot.
- [gemini-cli-extensions/ralph](https://github.com/gemini-cli-extensions/ralph) - Gemini CLI extension for Ralph loops.
- [opencode-ralph-loop](https://github.com/charfeng1/opencode-ralph-loop) - Minimal OpenCode plugin that auto-continues until the task is complete.
- [pi-ralph-wiggum](https://github.com/tmustier/pi-extensions/tree/main/pi-ralph-wiggum) - Pi extension for Ralph loops.
- [neuralyzer](https://github.com/gintasz/neuralyzer) - Pi tool that lets the agent wipe its own session context and resend the first message, putting loop control inside the agent.
- [ralph-for-kiro](https://github.com/laithalsaadoon/ralph-for-kiro) - Minimal Ralph CLI for Kiro CLI.

### Orchestrators and Interfaces

- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) - Multi-agent orchestration for Claude Code with a `/ralph` persistence mode and a `ralplan` planning stage.
- [ralph-tui](https://github.com/subsy/ralph-tui) - Terminal UI orchestrator connecting to task trackers, with interactive PRD creation.
- [LoopTroop](https://github.com/looptroop-ai/LoopTroop) - Local GUI that plans with an LLM council, runs OpenCode in isolated worktrees, retries from clean context on failure, and gates results on human approval.
- [compound-product](https://github.com/snarktank/compound-product) - Product loop that reads reports, picks priorities, and implements fixes with the Ralph pattern.

### SDKs and Libraries

- [ralph-loop-agent](https://github.com/vercel-labs/ralph-loop-agent) - Vercel's TypeScript SDK wrapper with verification callbacks and context summarization.

### Beyond Coding

- [ml-ralph](https://github.com/pentoai/ml-ralph) - Autonomous ML agent that runs experiments with Claude or Codex.
- [ralph-wiggum-marketer](https://github.com/muratcankoylan/ralph-wiggum-marketer) - Claude Code plugin that applies the Ralph loop to copywriting with research agents.

## Companion Tools

### Planning and Specs

- [lisa](https://github.com/blencorp/lisa) - Claude Code spec-interview workflow that produces the specs a Ralph loop executes.
- [bmalph](https://github.com/LarsCowe/bmalph) - BMAD-METHOD planning phases that hand off to snarktank/ralph for execution.

### Loop Control and Guardrails

- [MartinLoop](https://github.com/Keesan12/martin-loop) - Control plane for agent loops with budget stops, verifier gates, rollback evidence, and audit records.
- [antiburn](https://github.com/antiburn/antiburn) - Local desktop app that flags causes of token burn in agent sessions, such as overly deep sessions, broken caching, and unused tools.

## Vendor Guides

- [Goose Ralph Loop Tutorial](https://goose-docs.ai/docs/tutorials/ralph-loop/) - Block's Goose implementation with cross-model review and recipe-based workflows.
- [Copilot SDK Ralph Loop Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/nodejs/ralph-loop.md) - GitHub's recipe for building a Ralph loop with the Copilot SDK.
- [Kimi Agent SDK Ralph Loop Example](https://github.com/MoonshotAI/kimi-agent-sdk/tree/main/examples/go/ralph-loop) - Moonshot AI's Go example of a Ralph loop.
- [Claude Code Goals](https://code.claude.com/docs/en/goal) - Claude Code's built-in `/goal` loop, where an evaluator checks a completion condition after each turn.
- [Using Goals in Codex](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex) - OpenAI's cookbook for Codex `/goal`, its built-in run-until-done loop.

## Tutorials and Guides

- [Getting Started with Ralph](https://www.aihero.dev/getting-started-with-ralph) - Step-by-step quickstart with Claude Code and Docker by Matt Pocock.
- [11 Tips for AI Coding with Ralph Wiggum](https://www.aihero.dev/tips-for-ai-coding-with-ralph-wiggum) - AFK coding, human-in-the-loop Ralph, iteration caps, and progress tracking.
- [ralph-loop-quickstart](https://github.com/coleam00/ralph-loop-quickstart) - Cole Medin's quickstart for the bash-loop version, as an alternative to the plugin.
- [Ralph Wiggum Guide](https://github.com/JeredBlu/guides/blob/main/Ralph_Wiggum_Guide.md) - Community-written end-to-end guide.
- [The Ralph Wiggum Approach](https://dev.to/sivarampg/the-ralph-wiggum-approach-running-ai-coding-agents-for-hours-not-minutes-57c1) - Stop hook mechanism, troubleshooting, and Q&A.
- [Ryan Carson's Step-by-Step Guide](https://x.com/ryancarson/status/2008548371712135632) - Setting up and running snarktank/ralph, by its author.
- [How to Build an Effective Long Running Agent Loop in 7 Minutes](https://x.com/dabit3/status/2013091003104727338) - From spec to polished PRD to running the agent with Claude Code, Codex, or OpenCode.
- [Patterns for Running Unattended Work](https://stevekinney.com/courses/ai-development-setup/patterns-for-running-unattended-work) - Course lesson on Ralph loops, circuit breakers, human-gated autonomy, and worktree swarms.
- [Ralph Cursor Guide](https://forum.cursor.com/t/ralph-cursor-guide/149998) - Community guide to running Ralph in Cursor.

## Articles

- [A Brief History of Ralph](https://www.humanlayer.dev/blog/brief-history-of-ralph) - Timeline of the technique, including the Y Combinator hackathon story.
- [The Real Ralph Wiggum Loop](https://thetrav.substack.com/p/the-real-ralph-wiggum-loop-what-everyone) - Contrasts the original bash loop with the philosophy of the Anthropic plugin.
- [Entering the Mind of Ralph Wiggum](https://stevekinney.com/writing/the-ralph-loop) - Long-form explanation of the loop's mechanics and design choices.
- [The Ralph Wiggum Loop, from First Principles](https://www.dreamhost.com/blog/ralph-wiggum/) - External checks decide completion, state lives in the repo, and the agent is replaceable.
- [The 'Unpossible' Logic of Ralph Wiggum-Style AI Coding](https://tessl.io/blog/unpacking-the-unpossible-logic-of-ralph-wiggumstyle-ai-coding) - Analysis of the technique and the plugin controversy.
- [Ralph Loops Make Agentic Coding Reliable with Ruthless Context Resets](https://linearb.io/blog/dex-horthy-humanlayer-rpi-methodology-ralph-loop) - Dex Horthy on context resets and the Research-Plan-Implement method.
- [Self-Improving Coding Agents](https://addyosmani.com/blog/self-improving-agents/) - Addy Osmani on loop patterns for long-running agents.
- [Ralph Wiggum Explained: Tell It What Blocks You](https://platform.uno/blog/ralph-wiggum-explained-stop-telling-ai-what-you-want-tell-it-what-blocks-you/) - Framing prompts as backpressure instead of wishes.
- [The Ralph Wiggum Loop](https://www.codecentric.de/en/knowledge-hub/blog/the-ralph-wiggum-loop-autonomous-code-generation-with-a-fresh-context) - Autonomous code generation with a fresh context per iteration.
- [Decoding the New AI Lingo](https://github.blog/ai-and-ml/decoding-the-new-ai-lingo-loops-harnesses-squads-hill-climbing-oh-my/) - GitHub's glossary of loops, harnesses, and squads, including Ralph loops and their token cost.
- [Ralph Wiggum Explained: The Claude Code Loop That Keeps Going](https://blog.devgenius.io/ralph-wiggum-explained-the-claude-code-loop-that-keeps-going-3250dcc30809) - How the loop works and why.
- [Ralph Wiggum and AI Coding Loops](https://www.ishir.com/blog/312751/ralph-wiggum-and-ai-coding-loops-from-springfield-to-real-world-software-automation.htm) - From Springfield to real-world software automation.
- [2026: The Year of the Ralph Loop Agent](https://dev.to/alexandergekov/2026-the-year-of-the-ralph-loop-agent-1gkj) - Predictions on the Ralph loop's impact on development.

## Case Studies

Firsthand reports from running Ralph loops on real work.

- [We Put a Coding Agent in a While Loop](https://github.com/repomirrorhq/repomirror/blob/main/repomirror.md) - YC Agents hackathon report: a headless Claude Code loop ported 6 repositories overnight.
- [The Nightly Ralph Loop](https://cloudwired.dev/notes/the-nightly-ralph-loop) - Two weeks of an unattended loop turning GitHub issues into 82 PRs, with the guardrails and the numbers.
- [What I Learned Pointing a Ralph Loop at My Product for a Week](https://amplitude.com/blog/ralph-loop) - 102 verified features, and why verification and human judgment become the bottleneck.
- [Long-Running Claude for Scientific Computing](https://www.anthropic.com/research/long-running-claude) - Anthropic research using the Ralph loop to counter "agentic laziness" on long tasks.
- [Hardening RalphCI Loops](https://loop.circleci.com/hardening-ralphci-loops-for-open-source-after-the-february-2026-study) - CircleCI study where loops only finish on green CI, after local-only runs passed CI 1 time in 5.
- [How I Got Ralph to Ship Overnight](https://richtabor.com/ralph) - Rich Tabor's setup and results.
- [Ship Features in Your Sleep with Ralph Loops](https://www.geocod.io/code-and-coordinates/2026-01-27-ralph-loops) - Geocodio's engineering team running Ralph on a product codebase.
- [The Ralph Loop: How I Run Autonomous AI Agents Overnight](https://blakecrosley.com/blog/ralph-agent-architecture) - Stop hooks, spawn budgets, filesystem memory, and the failures along the way.

## Critiques

- [Ralph-Wiggum Is Bad and Anthropic Should Fix It](https://www.lesswrong.com/posts/bmNHsY5i3EoP4BAoJ/ralph-wiggum-is-bad-and-anthropic-should-fix-it) - Argues the plugin's coercive completion prompt conflicts with model honesty.
- [What Ralph Wiggum Loops Are Missing](https://xr0am.substack.com/p/what-ralph-wiggum-loops-are-missing) - Limits that appear when loops scale.
- [Ralph Wiggum Loops: The Downsides](https://h0bb3.github.io/log/ai/development/automation/2026/01/25/ralph-wiggum-loops-downsides.html) - Coherence loss, documentation drift, and cost from a real run.
- [Autonomous Loops Need a Scoring Function](https://understandingdata.com/posts/autonomous-loops-need-benchmarks/) - Why a loop needs a measurable objective, not just a completion signal.
- [Crypto Grifters Are Recruiting Open-Source AI Developers](https://www.seangoedecke.com/gas-and-ralph/) - Warning about token schemes riding on the technique's popularity.

## News

- [How Ralph Wiggum Went from The Simpsons to the Biggest Name in AI](https://venturebeat.com/technology/how-ralph-wiggum-went-from-the-simpsons-to-the-biggest-name-in-ai-right-now) - VentureBeat on the cultural phenomenon.
- ['Ralph Wiggum' Loop Prompts Claude to Vibe-Clone Commercial Software](https://www.theregister.com/2026/01/27/ralph_wiggum_claude_loops/) - The Register on cost claims and Huntley's concerns.
- [Thoughtworks Technology Radar: Ralph Loop](https://www.thoughtworks.com/radar/techniques/ralph-loop) - Placed in "Assess", noting fresh context per iteration at a high token cost.

## Videos

- [The Ralph Wiggum Loop from 1st Principles](https://www.youtube.com/watch?v=4Nna09dG_c0) - Geoffrey Huntley explains the technique himself.
- [Ralph Wiggum Showdown with Geoffrey Huntley](https://www.youtube.com/watch?v=SB6cO97tfiY) - Live coding demo, history, and bash loop vs. Stop hook implementations.
- [AI That Works: Ralph Wiggum](https://www.youtube.com/watch?v=fOPvAPdqgPo) - 75-minute session on why Ralph works: context windows, control loops, and applications.
- [Matt Pocock's Ralph Overview](https://www.youtube.com/watch?v=_IK18goX4X8) - Practical overview grounded in kanban and requirements discovery.
- [We Need to Talk About Ralph](https://www.youtube.com/watch?v=Yr9O6KFwbW4) - Theo's commentary on putting Claude Code in a while loop.
- [I Can't Believe Anthropic Messed Up the Ralph Wiggum](https://www.youtube.com/watch?v=XVAhQ-EcrWA) - Better Stack compares the plugin with the original loop.
- [Ralph Wiggum Is the Final Evolution of Vibe Coding](https://www.youtube.com/watch?v=5xvP9O4msLM) - Cole Medin's walkthrough, paired with his quickstart repository.
- [Ralph Wiggum Tutorial: How to Run It Safely and Efficiently](https://www.youtube.com/watch?v=eAtvoGlpeRU) - JeredBlu's companion to the written guide.
- [The Ralph Loop Explained](https://www.youtube.com/watch?v=CV97l0GkPHo) - Dan Vega's bash-loop walkthrough on a Java project.
- [What Ralph Wiggum Loop Really Is](https://www.youtube.com/watch?v=IS_naHhVeOo) - Three-minute explainer from the Goose team.

## Talks

- [Ralph Loops: Build Dumb AI Loops That Ship](https://www.youtube.com/watch?v=2TLXsxkz0zI) - Chris Parsons' AI Engineer Europe 2026 workshop on feedback loops, delivery contracts, and human review.
- [The Great Loops Debate](https://www.youtube.com/watch?v=c35YoMdnI78) - AI Engineer World's Fair 2026 debate with Geoffrey Huntley and Dex Horthy on loop hype versus practice.
- [The Ralph Wiggum Method Explained](https://gitnation.com/contents/the-ralph-wiggum-method-explained) - Eddy Vinck at AI Coding Summit 2026.

## Podcasts

- [Inventing the Ralph Wiggum Loop](https://linearb.io/dev-interrupted/podcast/inventing-the-ralph-wiggum-loop) - Dev Interrupted with Geoffrey Huntley on context rot, compaction, and the $10.42/hour calculation. A [transcript](https://devinterrupted.substack.com/p/inventing-the-ralph-wiggum-loop-creator) is available.
- [AI Giants: Geoffrey Huntley](https://www.youtube.com/watch?v=ZBkRBs4O1VM) - Codacy's long-form interview with the creator of Ralph.
- [Is Coding Over?](https://www.youtube.com/watch?v=ziXOV0b134s) - Geoffrey Huntley on loop engineering, part 1 of Josh Wulf's series.
- [Ralph Wiggum Coding Agent Power Tools](https://boundaryml.com/podcast/2025-10-28-ralph-wiggum-coding-agent-power-tools) - BoundaryML on tooling and advanced techniques.
- [Ralph Wiggum AI Agent Explained](https://www.youtube.com/watch?v=RpvQH0r0ecM) - The Startup Ideas Podcast with Ryan Carson, for founders and builders.
- [Ryan Carson Explains the Ralph Wiggum Loop](https://zeno.fm/podcast/tool-use-ai-conversations/episodes/ryan-carson-explains-the-ralph-wiggum-loop) - Tool Use podcast on implementing Ralph with Amp and Claude Code.

## Discussions

Hacker News threads.

- [Original HN Discussion](https://news.ycombinator.com/item?id=44565028) - The discussion that helped popularize the technique.
- [We Put a Coding Agent in a While Loop](https://news.ycombinator.com/item?id=45005434) - Huntley participated; security concerns raised about default passwords.
- [Ralph Wiggum as a Software Engineer](https://news.ycombinator.com/item?id=43817200) - Code quality critiques and maintainability debates.
- [Show HN: Continuous Claude](https://news.ycombinator.com/item?id=45938517) - Running Claude Code in a PR-and-CI loop.
- [Tips Discussion](https://news.ycombinator.com/item?id=46547129) - Community tips and experiences.
- [Ralph from First Principles](https://news.ycombinator.com/item?id=46587275) - Discussion of Huntley's explainer video.
- [What Happens After Ralph Wiggum?](https://news.ycombinator.com/item?id=46632445) - The future of autonomous coding patterns.
- [Crypto Grifters Are Recruiting Open-Source AI Developers](https://news.ycombinator.com/item?id=46654878) - Debate on the token scheme around Ralph.
- [A Brief History of Ralph](https://news.ycombinator.com/item?id=46682325) - Discussion of HumanLayer's timeline.
- [What Ralph Wiggum Loops Are Missing](https://news.ycombinator.com/item?id=46750937) - Debate on the limits of naive loops.

## Communities

- [r/RalphCoding](https://www.reddit.com/r/RalphCoding/) - Subreddit for sharing Ralph learnings, resources, and achievements.
- [Ralph Discord](https://discord.gg/MUyRMqKcWx) - Discord server discussing Ralph methods, resources, and achievements.

## Related Lists

- [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code#readme) - Skills, hooks, slash commands, and plugins for Claude Code.
- [Awesome Harness Engineering](https://github.com/walkinglabs/awesome-harness-engineering#readme) - Harnesses, loops, and environments for AI agents.
- [Awesome Claude: Ralph Wiggum](https://awesomeclaude.ai/ralph-wiggum) - Reference page with tips and configuration examples.

## Contributing

Contributions welcome! Read the [contribution guidelines](CONTRIBUTING.md) first.

## Footnotes

[![Star History Chart](https://api.star-history.com/svg?repos=snwfdhmp/awesome-ralph&type=Date)](https://www.star-history.com/#snwfdhmp/awesome-ralph&Date)
