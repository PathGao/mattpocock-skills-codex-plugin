# Matt Pocock Skills Codex Plugin

[中文说明](./README.zh-CN.md)

A Codex plugin package for selected skills from [mattpocock/skills](https://github.com/mattpocock/skills).

This repository is intended for public Codex plugin installation. It packages the skills as a native Codex plugin with `.codex-plugin/plugin.json` and a Codex marketplace manifest at `.agents/plugins/marketplace.json`.

## Source

- Upstream repository: [mattpocock/skills](https://github.com/mattpocock/skills)
- Current repository: [PathGao/mattpocock-skills-codex-plugin](https://github.com/PathGao/mattpocock-skills-codex-plugin)
- Upstream base: `mattpocock/skills` version `1.0.1`
- License: MIT, following the upstream project metadata

This package is derived from the upstream `1.0.1` content and removes the upstream `personal`, `deprecated`, and `in-progress` areas by default. The only `in-progress` skill currently restored is `review`, from upstream `skills/in-progress/review`, as a public-package exception. Upstream `misc/*` is not included because those skills are mostly tooling or Claude-specific guardrails and are not suitable as default Codex plugin skills. The plugin exposes the curated skills under the `mattpocock-skills` Codex namespace.

## Included Skills

- `ask-matt`
- `codebase-design`
- `diagnosing-bugs`
- `domain-modeling`
- `grill-me`
- `grill-with-docs`
- `grilling`
- `handoff`
- `implement`
- `improve-codebase-architecture`
- `prototype`
- `review`
- `setup-matt-pocock-skills`
- `tdd`
- `teach`
- `to-issues`
- `to-prd`
- `triage`
- `writing-great-skills`

## Install

In Codex, add this repository as a plugin marketplace, then install the plugin named `mattpocock-skills`.

```text
/plugin marketplace add PathGao/mattpocock-skills-codex-plugin
/plugin install mattpocock-skills
```

Installing it as a marketplace plugin lets Codex keep tracking this repository. When a newer version is available, Codex can manage the update through its plugin marketplace flow, including an upgrade button in surfaces that provide one.

If your Codex surface uses CLI commands instead of chat slash commands, use the equivalent plugin marketplace add and plugin install commands for that surface.

## Usage

After installation, skills are available with the `mattpocock-skills:` namespace.

Examples:

```text
mattpocock-skills:ask-matt
mattpocock-skills:to-prd
mattpocock-skills:to-issues
mattpocock-skills:tdd
mattpocock-skills:implement
mattpocock-skills:review
mattpocock-skills:handoff
```

`ask-matt` is the router skill. Use it when you want the plugin to choose a workflow for planning, critique, PRD writing, issue breakdown, teaching, handoff, or engineering diagnosis.

## Repository Layout

```text
.agents/plugins/marketplace.json  Codex marketplace entry
.codex-plugin/plugin.json         Codex plugin manifest
assets/                           Plugin icons
skills/                           Packaged skill directories
```

## Maintenance Notes

- Keep `.codex-plugin/plugin.json` version aligned with the packaged upstream base or the fork release version you choose.
- Keep `.agents/plugins/marketplace.json` plugin name aligned with `.codex-plugin/plugin.json`.
- Do not add upstream `personal`, `deprecated`, `misc`, or any other `in-progress` skill unless the public package policy changes. Currently, `review` is the only included `in-progress` skill.
- When pulling upstream updates, review every new skill before exposing it in this plugin.
