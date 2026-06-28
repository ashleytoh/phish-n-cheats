# phish-n-cheats — Claude Code skills bundle

A project-scoped bundle of [Claude Code skills](https://code.claude.com/docs/en/skills) that can be shared by cloning this repository. There is no package manager, build step, or install script required: open Claude Code from inside the repo and the skills under `.claude/skills/` are discovered automatically.

## Quick start

```bash
git clone https://github.com/ashleytoh/phish-n-cheats.git
cd phish-n-cheats
claude
```

Once Claude Code is running inside the repository, the bundled project skills are available for that session. To verify that they loaded, ask Claude what skills are available or invoke one directly, for example:

```text
/frontend-design
```

> **Scope:** these are project skills. They are active while you are working inside this repository, but they do not follow you into unrelated projects. For global usage, install a skill as a personal skill in `~/.claude/skills/` or use the upstream plugin where applicable.

## What is included

| Category | Skills | Use them for |
|---|---|---|
| UI and web design | `frontend-design`, `web-artifacts-builder` | Designing distinctive frontends and building rich claude.ai HTML artifacts with React, Tailwind, and shadcn/ui. |
| Integrations | `mcp-builder` | Building MCP servers that expose external APIs as clean, well-designed tools. |
| Testing | `webapp-testing` | Using Playwright to interact with local web apps, verify UI behavior, capture screenshots, and inspect browser logs. |
| Presentations | `frontend-slides` | Creating animation-rich, zero-dependency HTML presentations or converting slide concepts into polished web slides. |
| Engineering workflow | `brainstorming`, `writing-plans`, `executing-plans`, `subagent-driven-development`, `dispatching-parallel-agents`, `test-driven-development`, `systematic-debugging`, `verification-before-completion`, `requesting-code-review`, `receiving-code-review`, `using-git-worktrees`, `finishing-a-development-branch`, `writing-skills`, `using-superpowers` | Structuring engineering work from ideation through planning, execution, verification, review, and branch cleanup. |

## Skill sources

### From [anthropics/skills](https://github.com/anthropics/skills) — Apache-2.0

| Skill | What it is for |
|---|---|
| `frontend-design` | Distinctive, intentional visual design when building or reshaping UI, including aesthetic direction, typography, and avoiding templated defaults. |
| `mcp-builder` | Building high-quality MCP servers in Python/FastMCP or Node/TypeScript. |
| `web-artifacts-builder` | Elaborate multi-component claude.ai HTML artifacts using React, Tailwind, and shadcn/ui. |
| `webapp-testing` | Interacting with and testing local web apps via Playwright. |

### From [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) — MIT

| Skill | What it is for |
|---|---|
| `frontend-slides` | Animation-rich, zero-dependency HTML presentations from scratch or converted from PPT/PPTX. |

### From [obra/superpowers](https://github.com/obra/superpowers) — MIT

A library of engineering-workflow skills by Jesse Vincent, vendored here as plain Claude Code skills.

| Skill | What it is for |
|---|---|
| `brainstorming` | Explore intent, requirements, and design before creative or build work. |
| `writing-plans` | Turn a spec into a written, multi-step implementation plan. |
| `executing-plans` | Execute a written plan with review checkpoints. |
| `subagent-driven-development` | Execute plan tasks via independent subagents in the current session. |
| `dispatching-parallel-agents` | Coordinate two or more independent tasks with no shared state. |
| `test-driven-development` | Write tests before implementation for a feature or bugfix. |
| `systematic-debugging` | Work through bugs, test failures, and unexpected behavior methodically. |
| `verification-before-completion` | Require evidence, such as command output, before claiming work is done. |
| `requesting-code-review` | Check work against requirements before merging. |
| `receiving-code-review` | Handle review feedback with technical rigor rather than blind agreement. |
| `using-git-worktrees` | Isolate feature work in a dedicated workspace. |
| `finishing-a-development-branch` | Decide how to integrate completed work and clean up branches. |
| `writing-skills` | Create, edit, and verify Claude Code skills. |
| `using-superpowers` | Understand how the superpowers skills fit together. |

> **Note on superpowers:** upstream `obra/superpowers` is a plugin whose `SessionStart` hook can proactively dispatch skills. In this repository, the skills are vendored as plain project skills. They are still usable by name, but they do not auto-trigger at session start. For the full upstream plugin behavior, install it directly:
>
> ```text
> /plugin marketplace add obra/superpowers
> /plugin install superpowers
> ```

## Repository layout

```text
.claude/
  skills/
    <skill-name>/
      SKILL.md
      LICENSE or LICENSE.txt
      supporting files, if any
```

Each skill lives in its own folder. `SKILL.md` contains the skill metadata and instructions, while any supporting scripts, references, or assets should stay inside the same skill folder.

## Adding or updating a skill

1. Create or update `.claude/skills/<skill-name>/SKILL.md`.
2. Make sure the YAML frontmatter includes at least `name` and a clear `description` that explains when Claude should use the skill.
3. Keep supporting files such as `scripts/`, `references/`, and `assets/` inside that skill folder.
4. Preserve the upstream license file and attribution when vendoring a third-party skill.
5. Commit and push the change. Teammates can get the updated bundle with `git pull`.

See the [Claude Code skill authoring docs](https://code.claude.com/docs/en/skills) for the full skill format.

## Licenses and attribution

These skills are redistributed from their upstream repositories under their original licenses. Each skill folder keeps its corresponding license file.

- `frontend-design`, `mcp-builder`, `web-artifacts-builder`, `webapp-testing` — © Anthropic, Apache-2.0 — https://github.com/anthropics/skills
- `frontend-slides` — © 2025 Zara Zhang, MIT — https://github.com/zarazhangrui/frontend-slides
- All `superpowers` skills — © 2025 Jesse Vincent, MIT — https://github.com/obra/superpowers
