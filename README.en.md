<h1 align="center">project-to-skill</h1>

<p align="center"><strong>Turn real projects into installable, verifiable, reusable Codex Skills.</strong></p>

<p align="center">
  This is not a README-to-prompt rewriter. It connects source research, convertibility judgment, evidence extraction, strict validation, and secure packaging in one reproducible workflow.
</p>

<p align="center">
  <a href="README.md">简体中文</a> · <strong>English</strong> ·
  <a href="https://github.com/2025chunxi/project-to-skill/releases/tag/v0.1.0-beta">Download v0.1.0-beta</a> ·
  <a href="https://github.com/2025chunxi/project-to-skill/issues">Report an issue</a>
</p>

<p align="center">
  <a href="https://github.com/2025chunxi/project-to-skill/actions/workflows/ci.yml"><img alt="CI" src="https://github.com/2025chunxi/project-to-skill/actions/workflows/ci.yml/badge.svg"></a>
  <a href="https://github.com/2025chunxi/project-to-skill/releases/tag/v0.1.0-beta"><img alt="Release" src="https://img.shields.io/github/v/release/2025chunxi/project-to-skill?include_prereleases&style=flat-square"></a>
  <a href="LICENSE"><img alt="MIT License" src="https://img.shields.io/github/license/2025chunxi/project-to-skill?style=flat-square"></a>
  <img alt="Python 3.11+" src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=flat-square&logo=python&logoColor=white">
</p>

## Why This Exists

Strong models can write a `SKILL.md`. That does not mean the result is worth building, grounded in the source, installable, or safe to publish. Common failures include:

- Wrapping generic prompting in a Skill folder without testing whether conversion adds value.
- Guessing setup commands and usage examples without retaining source locations.
- Generating a near-duplicate of an already installed Skill.
- Leaking local paths, credential-like values, or unverified examples into release artifacts.
- Producing plausible files without strict validation, regression tests, or a working `.skill` package.

`project-to-skill` turns those failure points into a deterministic workflow and can explicitly recommend against low-value conversions.

```mermaid
flowchart LR
    A[Project / CLI / API / SOP / docs] --> B[Research sources]
    B --> C{Worth converting?}
    C -->|No| D[Explain the low-value verdict]
    C -->|Yes| E[Extract sourced setup and examples]
    E --> F[Generate Skill and evals]
    F --> G[Strict validation and security scan]
    G --> H[Installable .skill]
```

## Tested on a Real Project

An open-source test against [`encode/httpx@b5addb6`](https://github.com/encode/httpx/tree/b5addb64f0161ff6bfe94c124ef76f6a1fba5254) produced:

| Check | Result |
|---|---:|
| Files inspected | 123 |
| Skill conversion value | **90/100, high** |
| README setup commands extracted | **3**, each with section and line evidence |
| README usage examples extracted | **1 `pycon` example**, with source location |
| Capabilities detected | Python package, CLI, docs, tests, environment-variable names |
| Privacy behavior | Local source-project and installed-Skill paths omitted by default |

> `90/100` is a transparent heuristic conversion score, not a truth oracle. Retained commands and examples still need execution testing before publishing the generated Skill.

## What You Get

A high-value conversion creates a reviewable Skill source tree:

```text
skill-src/
├── SKILL.md
├── agents/openai.yaml
├── evals/evals.json
└── references/project-analysis.json
```

| Capability | What it solves |
|---|---|
| Project inspector | Detects ecosystems, package names, CLIs, tests, docs, environment names, and README usage |
| Convertibility score | Tests whether the Skill adds durable knowledge, fragile procedure, or reusable assets |
| Duplicate detection | Checks installed Skills for overlapping trigger scope |
| Source-backed extraction | Retains file, section, and line evidence for setup commands and examples |
| Guided generation | Produces `SKILL.md`, UI metadata, evals, and project analysis |
| Strict delivery | Validates, regression-tests, security-scans, and packages a `.skill` archive |

## Install in 30 Seconds

### Option 1: Ask Codex to install it

Send this in Codex:

```text
Use $skill-installer to install:
https://github.com/2025chunxi/project-to-skill/tree/main/skill/project-to-skill
```

Start a new task, then try:

```text
Use $project-to-skill to evaluate and convert path/to/project.
Decide whether it is worth turning into a Skill before generating, validating, and packaging it.
```

### Option 2: Download the release

Download [`project-to-skill.skill`](https://github.com/2025chunxi/project-to-skill/releases/download/v0.1.0-beta/project-to-skill.skill), extract its top-level `project-to-skill` directory into `$CODEX_HOME/skills` (default: `~/.codex/skills`), and start a new Codex task to load the Skill.

## Good Fits and Poor Fits

| Good candidate | Usually not worth a Skill |
|---|---|
| Stable API, CLI, SOP, template, or specialist method | Generic advice or ordinary prompting |
| Fragile sequence that is easy to repeat incorrectly | Mature models already perform it reliably without extra context |
| Project-specific commands, constraints, schemas, or assets | No reusable knowledge, script, or reference material |
| Deterministic validation, packaging, or privacy boundaries matter | Merely copying a README into `SKILL.md` |

## Build and Verify Locally

Requires Python 3.11+ and PyYAML 6.x:

```bash
python -m pip install -r requirements.txt
python scripts/build_release.py
```

The output is `dist/project-to-skill.skill`. The build runs README extraction tests, security regression tests, strict Skill validation, archive integrity checks, and repository-wide scans for secrets, PII, local paths, and unsafe archives.

## Privacy and Evidence Boundaries

- Generated artifacts omit absolute source-project and installed-Skill paths by default.
- Credential-like values are redacted; only environment-variable names are retained.
- `--include-local-paths` is for private local diagnostics and should not enter public artifacts.
- README extraction proves provenance, not successful execution.
- Conversion scoring supports judgment; release still requires realistic trigger tests and human review.

## Project Status

The current release is `v0.1.0-beta`. Deterministic inspection, validation, and packaging paths are covered by automated tests. Natural-language triggering will continue to be evaluated across Codex versions and project types.

Open an [Issue](https://github.com/2025chunxi/project-to-skill/issues) or read [CONTRIBUTING.md](CONTRIBUTING.md) to contribute.

## License

[MIT](LICENSE)
