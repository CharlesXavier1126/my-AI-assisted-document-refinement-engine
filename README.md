# my-AI-assisted-document-refinement-engine

A Claude Code skill that validates and improves your documents against a target repository. It reads relevant source files, identifies inaccuracies, missing details, and unclear sections, then produces a corrected markdown file.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and running

## How it works

1. **Analysis** — reads the document and relevant repository files silently
2. **Discussion** — presents findings and waits for your confirmation before writing anything
3. **Output** — writes `{filename}-refined.md` alongside the original document

## Usage

Run inside a Claude Code session:

```bash
/doc-refiner --doc <path-to-document> --repo <path-to-repository>
```

| Argument | Description |
|----------|-------------|
| `--doc`  | Path to the target document (`.txt` or `.md`) |
| `--repo` | Path to the repository or folder used as source of truth |

**Usage Example:**

```bash
/doc-refiner --doc ./docs/authentication.md --repo ./backend-repo
```

For example, to refine this current project `my-AI-assisted-document-refinement-engine`'s own README against its docs:

```bash
/doc-refiner --doc ./README.md --repo ./docs
```

## Skill file location

```
.claude/skills/doc-refiner/SKILL.md
```
