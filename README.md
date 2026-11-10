# Awesome EGM [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of plugins, ports, skills, tools and reading material for Google's **Elephant-Goldfish Model (EGM)**, the spec-driven, design-first workflow for AI coding agents.
>
> *Design with an elephant. Review with a goldfish.*

<p align="center">🐘 + 🐟</p>

**What is EGM?** EGM is not a language model. It is a set of skills and reviewer personas that sit on top of the coding agent you already use (Claude Code, Codex, Antigravity, Gemini CLI, Copilot and others). It separates three roles:

| Role            | Has access to                                                                 | Job                                                                               |
| --------------- | ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| 🐘 **Elephant** | Full project context and the whole design conversation                        | Interviews you, explores the problem, drafts the spec. Writes no production code. |
| 🐟 **Goldfish** | Only the spec and the files it references, with no memory of the conversation | Reviews the spec fresh to expose unstated assumptions, gaps and blind spots.      |
| 🧑 **You**      | Product goals, constraints and the review findings                            | Make the architectural trade-offs and approve the spec before implementation.     |

## Contents

- [Official](#official)
- [Ports and Adapters](#ports-and-adapters)
  - [Claude Code](#claude-code)
  - [GitHub Copilot](#github-copilot)
  - [Cursor](#cursor)
  - [Gemini CLI and Antigravity](#gemini-cli-and-antigravity)
  - [OpenCode](#opencode)
  - [Pi Coding Agent](#pi-coding-agent)
  - [DeepSeek Harness](#deepseek-harness)
  - [Hermes Agent](#hermes-agent)
  - [Other Harnesses and Installers](#other-harnesses-and-installers)
- [Independent Implementations and Skill Packs](#independent-implementations-and-skill-packs)
- [Forks and Extended Workflows](#forks-and-extended-workflows)
- [Bundles and Skill Stacks](#bundles-and-skill-stacks)
- [Spec-Driven Development Integrations](#spec-driven-development-integrations)
- [Tools and Utilities](#tools-and-utilities)
- [Domain-Specific Applications](#domain-specific-applications)
- [Inspired by EGM](#inspired-by-egm)
- [Learning Resources](#learning-resources)
  - [Origins](#origins)
  - [Articles and Guides](#articles-and-guides)
  - [News Coverage](#news-coverage)
  - [Videos](#videos)
  - [Demos and Explainers](#demos-and-explainers)
- [Community](#community)
- [Related Concepts](#related-concepts)
- [Related Awesome Lists](#related-awesome-lists)

---

## Official

- [google/elephant-goldfish-model](https://github.com/google/elephant-goldfish-model) - Google's open-source plugin for designing and reviewing software with agents (Apache-2.0). It supports Claude Code, Claude Cowork, Codex, ChatGPT desktop, Antigravity, Cursor, Gemini, OpenCode, Copilot and Muse.
  - [egm.dev](https://egm.dev) - Project website.
  - [Getting started](https://github.com/google/elephant-goldfish-model/blob/main/docs/getting_started.md) - First run, from brainstorm to approved spec.
  - [Harness guide](https://github.com/google/elephant-goldfish-model/blob/main/docs/harnesses.md) - Setup notes for each supported agent.
  - [Architecture](https://github.com/google/elephant-goldfish-model/blob/main/docs/designs/architecture.md) - EGM lifecycle and system design.
  - [FAQ](https://github.com/google/elephant-goldfish-model/blob/main/docs/faq.md) - Alternatives, review bottlenecks, velocity and other common questions.
  - [Muse integration](https://github.com/google/elephant-goldfish-model/blob/main/docs/muse.md) - Installing and running EGM in Muse.
  - [Releases](https://github.com/google/elephant-goldfish-model/releases) - Version history and changelogs. The latest release is v0.1.1 (Nov 6, 2026).
  - [ChatGPT plugin listing](https://chatgpt.com/plugins/plugins_6aeb90f47ec88191a3c107e01d3eb357) - Published EGM plugin for the ChatGPT and Codex desktop apps.
- [Introducing the Elephant-Goldfish Model plugin](https://opensource.googleblog.com/2026/10/introducing-elephant-goldfish-model-plugin.html) - Google Open Source Blog launch post (Oct 22, 2026).

**Built-in skills**

| Skill              | What it does                                                                            |
| ------------------ | --------------------------------------------------------------------------------------- |
| `egm-brainstorm`   | Tests an idea under a no-code rule and writes `concepts_brief.md`.                      |
| `egm-draft`        | Turns the brief or notes into a design document, `design_draft.md`.                     |
| `egm-review`       | Runs a five-stage review with fresh Goldfish agents.                                    |
| `egm-resolve`      | Works through the review findings and agrees on changes.                                |
| `egm-review-loop`  | Runs a chosen group of reviewers against chosen standards. Works for any document type. |
| `egm-bootstrap`    | Creates or updates design docs for an existing codebase.                                |
| `egm-drift-report` | Compares checked-in docs with the current source code.                                  |

**Quick install**

```bash
# Claude Code
claude plugin marketplace add google/elephant-goldfish-model
claude plugin install egm@egm

# Codex
codex plugin marketplace add google/elephant-goldfish-model
codex plugin add egm@egm

# Antigravity CLI (in the Antigravity App or VS Code extension, run /plugin)
agy plugin install https://github.com/google/elephant-goldfish-model

# Muse (installs from a local clone)
git clone https://github.com/google/elephant-goldfish-model.git
muse plugins install ./elephant-goldfish-model --scope user
muse plugins approve egm
```

On the ChatGPT or Codex desktop app, install the published plugin listing linked above. For Claude Cowork, ChatGPT Work, Cursor, Gemini CLI, OpenCode and Copilot, follow the harness guide linked above. In Claude Code and Antigravity, skills use the `/egm:` prefix, for example `/egm:egm-brainstorm`.

> ⚠️ Brainstorm and review need an agent that can start fresh subagents. A review that runs in the same context "is not a Goldfish review", so EGM stops instead.

## Ports and Adapters

Community projects that bring EGM to other agents and harnesses. Unless a project says otherwise, it is unofficial.

### Claude Code

- [kurcontko/egm-claude-code](https://github.com/kurcontko/egm-claude-code) - Claude Code plugin for spec-driven development with isolated Goldfish reviews.
- [Raj9914/elephant-goldfish](https://github.com/Raj9914/elephant-goldfish) - Fresh-context subagents check your bug diagnosis, design doc and diff before you commit. Works with Claude Code, Codex and Gemini CLI.
- [techpeerPat/elephant-goldfish-skills](https://github.com/techpeerPat/elephant-goldfish-skills) - Design-first Elephant and Goldfish skills for Antigravity and Claude Code.

### GitHub Copilot

- [vt-bg/egm-copilot](https://github.com/vt-bg/egm-copilot) - Installs EGM into Copilot with 7 skills and 9 zero-context Goldfish reviewer agents, for JetBrains IDEs, VS Code and Copilot CLI.
- [jheo4/elephant-goldfish-copilot](https://github.com/jheo4/elephant-goldfish-copilot) - EGM template for Copilot in VS Code, with zero-context review, no-code gates and extensible packs.

### Cursor

- [jhincapie/egm-cursor](https://github.com/jhincapie/egm-cursor) - Unofficial Cursor port of the EGM skills.

### Gemini CLI and Antigravity

- [therealr2d2/elephant-goldfish-workflow-skill](https://github.com/therealr2d2/elephant-goldfish-workflow-skill) - Native Gemini CLI skill with a stateless Goldfish that runs in a sandbox and an adversarial reviewer. Also tuned for Antigravity.

### OpenCode

- [AzadKshitij/opencode-egm](https://github.com/AzadKshitij/opencode-egm) - OpenCode V2 adapter that bundles the EGM skills and reviewer personas into one self-contained package.
- [oli-nelson/EGM-OpenCode-V2](https://github.com/oli-nelson/EGM-OpenCode-V2) - Experimental OpenCode V2 plugin with the `egm` agent, read-only reviewers, skills and commands.
- [notsatyarth/opencode-egm](https://github.com/notsatyarth/opencode-egm) - EGM plugin for OpenCode v2.
- [jope35/opencode-egm](https://github.com/jope35/opencode-egm) - OpenCode plugin for the Elephant-Goldfish Model.

### Pi Coding Agent

- [sdsheeks/pi-egm](https://github.com/sdsheeks/pi-egm) - EGM for pi: design with context, review with fresh-context Goldfish reviewers.
- [nsanta/pi-elephant-goldfish](https://github.com/nsanta/pi-elephant-goldfish) - A deep-context Elephant drafts specs and zero-context Goldfish stress-test them.
- [thesawdawg/pi-egm](https://github.com/thesawdawg/pi-egm) - Pi-compatible plugin built from the Google repo.

### DeepSeek Harness

- [dryw/dsh-egm](https://github.com/dryw/dsh-egm) - EGM for DeepSeek Harness, published on npm as `dsh-egm`. A context-rich session drafts the spec and fresh read-only agents review it.
- [DSH-Extensions-list/dsh-elephant-goldfish-model](https://github.com/DSH-Extensions-list/dsh-elephant-goldfish-model) - Standalone EGM skills and fresh-context review workflows, installable from the DSH Plugin Hub as a `.tgz` release.
- [dannielcordeiro/dsh-egm](https://github.com/dannielcordeiro/dsh-egm) - Upstream EGM unchanged, plus per-role model routing and a live run view in the terminal and the browser.
- [marcelosf80/dsh-elephant-goldfish](https://github.com/marcelosf80/dsh-elephant-goldfish) - EGM skills as an installable DeepSeek Harness bundle.
- [uzair-suria/dsh-egm](https://github.com/uzair-suria/dsh-egm) - EGM workflows as DSH skills and Agent Presets, generated from the upstream repo.
- [643048695/dsh-egm](https://github.com/643048695/dsh-egm) - Design-review gate for DSH: the Elephant drafts, zero-context Goldfish attack the draft, and you approve.

### Hermes Agent

- [willbohn/hermes-egm](https://github.com/willbohn/hermes-egm) - Design reviews for Hermes Agent, with fresh-context, tool-free reviewers and checked citations.

### Other Harnesses and Installers

- [yathamsriram243-blip/egm-universal-agent](https://github.com/yathamsriram243-blip/egm-universal-agent) - Universal EGM skills, slash commands and review subagents, with cross-agent adapters and automated validation.
- [sufiyan-sabeel/indus-egm](https://github.com/sufiyan-sabeel/indus-egm) - Rust CLI and library, installable with cargo, that embeds the EGM bundle and installs it into a coding agent.
- [Jehu/bb-elephant-goldfish](https://github.com/Jehu/bb-elephant-goldfish) - EGM for BB.
- [Semdok/semdok-egm](https://github.com/Semdok/semdok-egm) - Plan features before coding: brainstorm, draft a design, and review it with fresh-context reviewers.

## Independent Implementations and Skill Packs

Takes on the Elephant/Goldfish pattern that don't depend on Google's plugin.

- [vshvedov/elephant-goldfish](https://github.com/vshvedov/elephant-goldfish) - Reusable workflow for Claude Code, Codex and Gemini CLI. It covers brainstorming, features, bug fixes and code review. The most-starred community project as of November 2026.
- [marcus-darden/egm](https://github.com/marcus-darden/egm) - EGM as Agent Skills: design-first skills, a fresh-context doc review, guarded implementation and a strict code review.
- [donchummar/elephant-goldfish-skill](https://github.com/donchummar/elephant-goldfish-skill) - Agent skill for Claude Code, Codex or Gemini CLI that makes the AI write a design doc, then has zero-context agents prove it is buildable before implementation starts.
- [samsauhard/elephant-goldfish-harness](https://github.com/samsauhard/elephant-goldfish-harness) - Python agent harness with isolated design reviewers, bounded retries, trace logs and reproducible evaluation fixtures.
- [ldsAS/elephant-goldfish-skill](https://github.com/ldsAS/elephant-goldfish-skill) - 🇹🇼 Tool-neutral agent skill with four-role separation, CUJ-driven development and objective validation scripts. Works with Claude Code, Antigravity and Cursor.
- [Sam-Si/skills](https://github.com/Sam-Si/skills) - MIT-licensed agent skills collection whose first skill is EGM.
- [Fallenstedt/refined-elephant-goldfish](https://github.com/Fallenstedt/refined-elephant-goldfish) - Skills that help you understand the problem before you build a solution.
- [chienweiluo/eg-skills](https://github.com/chienweiluo/eg-skills) - A personal Elephant/Goldfish engineering workflow.

## Forks and Extended Workflows

- [gsVAM/SuperEGM](https://github.com/gsVAM/SuperEGM) - Merges superpowers and EGM into one Claude Code plugin: brainstorm, spec review, plan and more.
- [debashisn94/egm-aios](https://github.com/debashisn94/egm-aios) - Claude Code fork with Sonnet reviewers, approve-before-spawn and auto-routing.
- [bhubbard/elephant-goldfish-model-rs](https://github.com/bhubbard/elephant-goldfish-model-rs) - Copy of the official plugin that adds native Rust `egm` and `goldfish` CLIs.

## Bundles and Skill Stacks

Projects that ship EGM next to other skill packs so you install everything at once.

- [claudemods/context-forge](https://github.com/claudemods/context-forge) - One Claude Code plugin with 21 skills, including the EGM design and review skills, behind a single `/context-forge:forge` router.
- [thanhNt16/omp-precision-stack](https://github.com/thanhNt16/omp-precision-stack) - One-command installer for Oh My Pi that symlinks the vshvedov Elephant/Goldfish skills alongside Matt Pocock's skills, pstack and Superpowers.

## Spec-Driven Development Integrations

EGM combined with other spec-driven development (SDD) frameworks.

- [lutfi-zain/openspec-schema-egm](https://github.com/lutfi-zain/openspec-schema-egm) - EGM as a schema for [OpenSpec](https://github.com/Fission-AI/OpenSpec), published on npm as `openspec-schema-egm`.
- [vanguard-lint/vanguard-spec](https://github.com/vanguard-lint/vanguard-spec) - Spec verification harness, designed around EGM, that locks down architectural invariants before code is written and shows when specs go stale.
- [rariasdev/architechai-plugin](https://github.com/rariasdev/architechai-plugin) - 🇪🇸 Claude Code plugin that interviews you like a senior architect, writes a phased plan and turns it into a kanban of EGM-based prompts.

## Tools and Utilities

- [@rizkiaprita/egm](https://www.npmjs.com/package/@rizkiaprita/egm) - npm package for drafting specs, reviewing designs and checking implementation drift.
- [Dimoncelli/cold-jury](https://github.com/Dimoncelli/cold-jury) - Zero-dependency Node.js CLI with a cross-CLI review gate inspired by EGM. It runs sterile, hostile reviews to catch bugs the authoring agent would agree with.
- [arcobaleno64/seven-sec](https://github.com/arcobaleno64/seven-sec) - Stateless pre-commit git-diff gate. A zero-context Goldfish reviewer (Antigravity or Codex) blocks bugs, security issues and drift.

## Domain-Specific Applications

EGM applied outside ordinary software specs, often through `egm-review-loop` with custom reviewers.

- [OzaLabCP/talk-elephants-goldfish](https://github.com/OzaLabCP/talk-elephants-goldfish) - 🎤 Plan and review talks and lectures. Fresh reviewers check what an audience can follow and where it needs more context.
- [casali10/egm-campaign](https://github.com/casali10/egm-campaign) - 🎲 Tabletop RPG campaign prep in eight steps, checked by Goldfish reviewers. Claude Code plugin.
- [bmtrnavsky/spec-driven-data-analysis](https://github.com/bmtrnavsky/spec-driven-data-analysis) - 📊 Data analysis plugin for Hermes with locked specs, a sealed kernel, Goldfish review and provenance on every report.
- [GitGudAK/egm-eyewear-reviewers](https://github.com/GitGudAK/egm-eyewear-reviewers) - 👓 Specialist reviewer prompts for eyewear design.
- [ai-summer2025/google-egm-clinical-protocol-designer](https://github.com/ai-summer2025/google-egm-clinical-protocol-designer) - 🏥 Adversarial review loop for clinical trial protocol design, in pure Python with no paid APIs.
- [ai-summer2025/hedis-care-gap-agent](https://github.com/ai-summer2025/hedis-care-gap-agent) - 🏥 HEDIS care-gap closure agent with EGM adversarial review.
- [siriani/elephant-referee-model](https://github.com/siriani/elephant-referee-model) - 🔬 Write research with an Elephant and have zero-context Goldfish referee it, like peer review for scientific work.
- [linuxsunil/id-spec-studio](https://github.com/linuxsunil/id-spec-studio) - 🎓 Course design pipeline for instructional designers: brainstorm, draft, then four parallel Goldfish reviewers lock the spec.
- [PaulBratslavsky/strapi-product-egm](https://github.com/PaulBratslavsky/strapi-product-egm) - Plan a Strapi product. Adds fresh-context reviews to the strapi-product-builder interview.

## Inspired by EGM

Projects that build on the fresh-context review idea and add their own roles or loops.

- [sherol/squirrels](https://github.com/sherol/squirrels) - Adds Squirrels to the pattern: bounded, autonomous delegates that forage, cache findings and report back. Runs on top of the official plugin or vshvedov/elephant-goldfish.
- [roomi-fields/roomis-grillhouse](https://github.com/roomi-fields/roomis-grillhouse) - Claude Code framework where a "grill" settles the architecture, then fresh agents write tests and code and review them.
- [Mgabr90/autonomous-delivery](https://github.com/Mgabr90/autonomous-delivery) - Autonomous plan, design-review, build, review and fix loop with fresh-eyes review and an independent gate.
- [asteria-core/biome](https://github.com/asteria-core/biome) - Multi-agent software engineering ecosystem with Elephant, Goldfish, Beaver and Woodpecker roles.

## Learning Resources

### Origins

- [Elephants, Goldfish, and the New Golden Age of Software Engineering](https://medium.com/@drensin/elephants-goldfish-and-the-new-golden-age-of-software-engineering-c33641a48874) - Dave Rensin's original essay.
- [Google Research publication page](https://research.google/pubs/elephants-goldfish-and-the-new-golden-age-of-software-engineering/) - The essay as a Google Research paper.
- [ChocoTrail/elephant_goldfish](https://github.com/ChocoTrail/elephant_goldfish) - Summary of Rensin's essay.

### Articles and Guides

- [Elephant-Goldfish Design Review](https://agentpatterns.ai/patterns/multi-agent/elephant-goldfish-design-review/) - Agent Patterns entry that maps each claim to the repo source.
- [Google's Elephant-Goldfish Model: Review the Plan Before Code](https://wavect.io/blog/elephant-goldfish-model-design-review/) - Wavect deep dive on the five review stages, limits and a team pilot. Also available in [DE](https://wavect.io/de/blog/elephant-goldfish-model-design-review/), [ES](https://wavect.io/es/blog/elephant-goldfish-model-design-review/) and [ZH](https://wavect.io/zh/blog/elephant-goldfish-model-design-review/).
- [Google's Elephant Goldfish Model (EGM): What It Is and How It Works](https://www.mindstudio.ai/blog/google-elephant-goldfish-model-egm/) - MindStudio explainer.
- [Google's Elephant-Goldfish Method for AI Design Reviews](https://www.digitalapplied.com/blog/google-elephant-goldfish-agent-design-review) - Digital Applied overview.
- [Elephant-Goldfish Model (EGM): the free Google plugin that makes AI coding agents design first](https://aicon-hub.github.io/posts/egm-elephant-goldfish-model-google-open-source-spec-driven-development-plugin-guide.html) - AIcon Hub guide to spec-driven development with the plugin.
- [Google's Elephant-Goldfish Model: Let a Forgetful AI Check Your Plan Before You Build It](https://medium.com/@vinayanand2/googles-elephant-goldfish-model-let-a-forgetful-ai-check-your-plan-before-you-build-it-5ebc6baa52fd) - Medium introduction.
- [EGM Plugin: Installation in Claude Code and Codex, Workflow, and Use Cases](https://smartscope.blog/en/blog/elephant-goldfish-model-egm-plugin-installation-claude-code-2026/) - SmartScope install guide.
- [The Elephant-Goldfish Model: Why the AI That Knows Least Reviews Best](https://towardsai.com/p/machine-learning/the-elephant-goldfish-model-why-the-ai-that-knows-least-reviews-best) - Towards AI deep dive.
- [EGM: Design and Review Skills for AI Coding Agents](https://www.beri.net/learning/google-elephant-goldfish-model-egm-docs) - Beri learning page.
- [caleonardo/egm-ganular-steps](https://github.com/caleonardo/egm-ganular-steps) - A granular, manual step-by-step way to apply EGM with any chat tool and no plugins, with a diagram.
- [sou350121/Agent-Playbook](https://github.com/sou350121/Agent-Playbook) - 🇨🇳 Chinese engineering playbook for AI agents, with a theory module on EGM subagents.

### News Coverage

- [Google open-sources the EGM plugin its engineers use to catch AI coding mistakes](https://helpnetsecurity.com/2026/10/26/google-elephant-goldfish-model-plugin) - Help Net Security.
- [Google open sources its Elephant-Goldfish Model plugin for AI coding](https://betanews.com/article/google-open-sources-its-elephant-goldfish-model-plugin-for-ai-coding/) - BetaNews.
- [How Google's Elephant-Goldfish Model Revolutionises AI Coding Reliability](https://www.opensourceforu.com/2026/10/googles-elephant-goldfish-model-revolutionises-ai-coding-reliability/) - Open Source For You.
- [Google Open-Sources the Elephant-Goldfish Model Plugin Its Engineers Use to Catch AI Coding Mistakes](https://www.linuxtoday.com/blog/google-open-sources-the-elephant-goldfish-model-plugin-its-engineers-use-to-catch-ai-coding-mistakes/) - Linux Today.
- [Google AI Releases Elephant-Goldfish Model Plugin for Spec-First Coding](https://www.marktechpost.com/2026/11/08/google-elephant-goldfish-model-plugin-spec-review-coding-agents/) - MarkTechPost.
- [Elephants, Goldfish and the New Golden Age of Software Engineering](https://www.i-programmer.info/news/145-mapping-a-gis/18932-elephants-goldfish-and-the-new-golden-age-of-software-engineering.html) - I Programmer coverage of Rensin's paper.

### Videos

- [Google Just Open Sourced Its AI Coding Secret: Elephant Goldfish Model](https://www.youtube.com/watch?v=6zQ2xIXpLa8) - Overview of the plugin and spec-driven development with coding agents.
- [O novo jeito de programar com IA que o Google usa, agora no Claude Code](https://www.youtube.com/watch?v=niRV-yuu5q4) - 🇧🇷 EGM with Claude Code, in Portuguese.
- [Elephant Goldfish Modelとは？ AIの設計を別の視点で見直すGoogleの手法](https://www.youtube.com/watch?v=jZJltc_vjUA) - 🇯🇵 Podcast episode on reviewing a design before implementation, in Japanese.

### Demos and Explainers

- [gsaini/egm-getting-started](https://github.com/gsaini/egm-getting-started) - Runs EGM end to end on a real codebase: brainstorm, draft, the five-stage Goldfish review, then resolve.
- [Elephant-Goldfish Model: Review the Plan Before AI Writes Code](https://www.ai.joaoqueiros.com/blog/elephant-goldfish-model-claude-code-spec-review-ai-labs) - Notes on AI Labs' walkthrough of EGM on a demo app.
- [sateesh2020/egm-goldfish-experiment](https://github.com/sateesh2020/egm-goldfish-experiment) - Reproducible experiment: a toy codebase and a design doc with seven planted flaws, testing whether zero-context Goldfish reviews catch more than a same-context review.
- [neuralmind-ai/eg-demo](https://github.com/neuralmind-ai/eg-demo) - Demo of the elephant-goldfish method.
- [rodolfochicone/egm-skills-map](https://github.com/rodolfochicone/egm-skills-map) - 🇧🇷 Interactive map of the EGM plugin skills for Claude Code.

## Community

- [GitHub Issues](https://github.com/google/elephant-goldfish-model/issues) - Bug reports and feature requests.
- [GitHub Discussions](https://github.com/google/elephant-goldfish-model/discussions) - Questions and ideas.
- [Releases feed](https://github.com/google/elephant-goldfish-model/releases.atom) - Atom feed for new releases. You can also use Watch → Custom → Releases on GitHub.

## Related Concepts

**Spec-Driven Development (SDD).** EGM puts SDD into practice: you write, review and approve the spec *before* implementation starts. "Design is the new code." Other SDD frameworks include [GitHub Spec Kit](https://github.com/github/spec-kit) and [OpenSpec](https://github.com/Fission-AI/OpenSpec).

**Context isolation in multi-agent systems.** EGM's core idea is a hard split between the Elephant, which holds all the context, and stateless Goldfish reviewers. The split prevents *context collapse*, where a model treats what it remembers as obvious from the text and ends up confirming its own faulty assumptions.

**Adversarial and hostile review.** Goldfish act as critics hunting for edge cases, hidden dependencies and logic gaps. This is the same idea behind "jury" and red-team review tools.

## Related Awesome Lists

- [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) - Tools and resources for Claude Code.
- [awesome-codex](https://github.com/jqueryscript/awesome-codex) - Tools, skills and plugins for OpenAI Codex.
- [awesome-claude-plugins](https://github.com/Chat2AnyLLM/awesome-claude-plugins) - Claude marketplaces and plugins.
- [awesome-claude-skills](https://github.com/Chat2AnyLLM/awesome-claude-skills) - Claude skills.
- [awesome-deepseek-harness](https://github.com/awesome-deepseekharness/awesome-deepseek-harness) - DeepSeek Harness plugins, tools and skills.
- [awesome-ai-agents](https://github.com/aloth/awesome-ai-agents) - AI agent frameworks, tools and research.

## Contributing

The EGM ecosystem is young, and contributions are welcome. Read the [contribution guidelines](CONTRIBUTING.md), then open a PR that adds the link in the right section, in this format:

```markdown
- [owner/repo](https://github.com/owner/repo) - Short description ending with a period.
```

Please only add projects that are public, have a README, and relate clearly to the Elephant-Goldfish pattern. Empty forks and mirrors won't be accepted.

---

This list is community-maintained and isn't affiliated with Google. EGM is "not an officially supported Google product."

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
