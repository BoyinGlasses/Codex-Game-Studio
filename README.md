# Codex Game Studio

**Turn OpenAI Codex into your AI game development studio.**

Plan, prototype, build, review, and ship games with coordinated AI specialists and reusable workflows.

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE) [![74 Skills](https://img.shields.io/badge/workflows-74-green.svg)](skills/) [![49 Agents](https://img.shields.io/badge/agent_roles-49-blueviolet.svg)](assets/template/.codex/agents/)

*An unofficial Codex adaptation of [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) by Donchitos.*

## Why Codex Game Studio?

Building a game with one AI assistant can get messy: design decisions disappear into chat history, implementation drifts from the original idea, and testing happens too late. The original [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) project addresses this with a studio hierarchy, specialist roles, and quality checkpoints.

**Codex Game Studio brings that structure to OpenAI Codex.** It provides a workflow from the first game idea to a playable build while keeping you responsible for decisions and verification. This is a set of skills and a starter template, not a game engine or finished game.

## What's included?

| Component | Count | Purpose |
| --- | ---: | --- |
| Workflow skills | 74 | Design, architecture, implementation, QA, and release |
| Specialist roles | 49 | Directors, department leads, and domain specialists |
| Project rules | 13 | Coding and design conventions routed through `AGENTS.md` |
| Starter template | 1 | Project structure for Godot, Unity, or Unreal |
| Codex hooks | Included | Session and validation hooks with a Codex adapter |

The plugin also provides `$ccgs-new-game` to create a new project. Skill names keep the `$ccgs-*` prefix for compatibility with existing workflows.

## Getting started

### Requirements

- [OpenAI Codex](https://developers.openai.com/codex/) with plugin support
- [Git](https://git-scm.com/)
- For bundled validation scripts: **Python 3** and **Bash** (Git Bash on Windows)

### 1. Install the plugin

Run in a terminal:

```powershell
codex plugin marketplace add BoyinGlasses/Codex-Game-Studio
codex plugin add codex-game-studio@codex-game-studio
```

Start a **new Codex task** after installing so Codex loads its skills.

### 2. Create a game project

In Codex, run:

```text
$ccgs-new-game Create a project at D:\Games\MyGame
```

Open `D:\Games\MyGame` as a **new Codex project**. Codex can then load its generated `AGENTS.md`, workflow skills, agent definitions, and hook configuration.

### 3. Start the guided workflow

```text
$ccgs-start
```

The onboarding workflow asks about your game idea or existing work, then helps choose the next step. Already building a game? Open its root folder in Codex and run `$ccgs-start` there. Use `$ccgs-help` to browse other workflows.

## From an idea to a game

```text
Idea -> Design -> Architecture -> Stories -> Code -> QA -> Release
  ^                                                        |
  +---------------------- Iterate -------------------------+
```

Some common entry points:

| Goal | Codex skill |
| --- | --- |
| Find the right next step | `$ccgs-start` or `$ccgs-help` |
| Explore an idea | `$ccgs-brainstorm` |
| Set up your game engine | `$ccgs-setup-engine` |
| Break down game systems | `$ccgs-map-systems` |
| Plan features | `$ccgs-create-epics` and `$ccgs-create-stories` |
| Implement a story | `$ccgs-dev-story` |
| Check code and readiness | `$ccgs-code-review` and `$ccgs-gate-check` |
| Prepare a release | `$ccgs-release-checklist` |

### Choose how much process you need

The generated `project.yaml` supports three `modes.rigor` levels:

| Level | Best for | Typical workflow |
| --- | --- | --- |
| `minimal` | Game jams and prototypes | Engine setup -> one-page brief -> stories -> code |
| `standard` | Games with connected systems | Design docs, architecture, development, QA |
| `full` | Larger projects and teams | Detailed planning, reviews, and evidence |

`$ccgs-start` helps choose a level; `$ccgs-settings` can adjust it later. `modes.automation` separately controls how often the workflow pauses for input.

## Studio hierarchy

The 49 specialist roles in the bundled template follow three tiers inspired by the upstream project:

```text
Directors
  creative-director   technical-director   producer
         |
Department leads
  game-designer   lead-programmer   art-director   qa-lead   ...
         |
Specialists
  gameplay-programmer   level-designer   sound-designer   ui-programmer   ...
```

Definitions live in [`assets/template/.codex/agents/`](assets/template/.codex/agents/). Codex can delegate to these roles when agent delegation is available; otherwise it can use the role instructions directly. Naming a role does not mean a separate agent ran.

### Supported engines

| Engine | Focus areas |
| --- | --- |
| **Godot 4** | GDScript, shaders, GDExtension |
| **Unity** | C#, DOTS/ECS, UI Toolkit, Addressables |
| **Unreal Engine 5** | C++, Blueprints, GAS, replication |

You still need to install your chosen engine to build and playtest a game.

## Repository structure

```text
Codex-Game-Studio/
|-- skills/                    # Plugin workflows ($ccgs-*)
|   +-- ccgs-new-game/         # Creates a new project
|-- assets/template/           # Files copied into a game project
|   |-- AGENTS.md              # Active Codex instructions
|   |-- project.yaml           # Engine and workflow configuration
|   |-- .agents/skills/        # 74 game workflows
|   |-- .codex/agents/         # 49 agent role definitions
|   |-- .codex/hooks.json      # Hook configuration
|   |-- .codex/hooks/          # Codex hook adapter
|   +-- .claude/               # Retained upstream source resources
|-- .agents/plugins/           # Marketplace metadata
|-- plugin.json                # Plugin manifest
+-- tests/smoke_port.py        # Port and hook smoke test
```

In a created game project, `AGENTS.md` governs Codex and `project.yaml` holds workflow configuration. The upstream `CLAUDE.md` remains as source reference.

## How the Codex port differs

The upstream project was created for **Claude Code**. This port maps `/name` workflows to **Codex `$ccgs-name` skills**, adapts specialist roles into **Codex agent TOML** files, and bridges supported scripts into **Codex hooks**.

Some original features have no direct Codex equivalent: Claude Code's `Notification` event and status line are not installed. Project hooks require compatible runtime support and may need trust through `/hooks`. On Windows, Git Bash and Python 3 are required for the original shell checks.

See [Codex port notes](assets/template/CODEX-PORT.md). The port is based on upstream commit [`d056997`](https://github.com/Donchitos/Claude-Code-Game-Studios/commit/d05699707fae39a9b3c78f4b5f69eb77819094f1); later upstream changes may not yet be included.

## Contributing

Suggestions, bug reports, engine compatibility fixes, and documentation improvements are welcome via [issues](https://github.com/BoyinGlasses/Codex-Game-Studio/issues) or [pull requests](https://github.com/BoyinGlasses/Codex-Game-Studio/pulls).

After changing a skill, role, or hook, run:

```powershell
python tests/smoke_port.py
```

## Credits and license

**Codex Game Studio** adapts **[Claude Code Game Studios by Donchitos](https://github.com/Donchitos/Claude-Code-Game-Studios)**. Donchitos created the original workflows, studio roles, templates, and rules; this repository adapts them for Codex. This is an **unofficial community port**, not affiliated with or endorsed by the original author.

Licensed under **MIT**. See [LICENSE](LICENSE) and [NOTICE.md](NOTICE.md) for the license and attribution.
