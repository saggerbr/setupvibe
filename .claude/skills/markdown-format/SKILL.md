---
name: markdown-format
description: Enforce and apply SetupVibe Markdown formatting standards when creating or editing any .md file in the repository.
metadata:
  short-description: Format project Markdown files
---

# Markdown Format

Apply the SetupVibe Markdown rules to every `.md` file you create or edit, and verify **all** Markdown files in the repository recursively.

## Source of Truth

All formatting rules, markdownlint rule IDs, configuration values, and examples are defined in [`MARKDOWN.md`](../../../MARKDOWN.md) at the project root. **Read that file before applying rules.** Do not derive rules from `CLAUDE.md`, `AGENTS.md`, or any other file — `MARKDOWN.md` is authoritative.

The markdownlint configuration is in [`.markdownlint.json`](../../../.markdownlint.json).

## Recursive Verification — Full Repository Scan

When invoked, this skill must scan **all** `.md` files in the repository recursively, not just the files directly modified by the current task.

### Step 1 — Discover all Markdown files

Use Claude Code `Glob` to find every `.md` file in the project:

```text
Pattern: **/*.md
```

This includes (but is not limited to):

- Root context files: `CLAUDE.md`, `AGENTS.md`, `MARKDOWN.md`, `CHANGELOG.md`, `README.md`, `CONTRIBUTING.md`
- `docs/**/*.md` — all languages (`en/`, `pt-br/`, `es/`, `fr/`) and all subdirectories
- `.claude/skills/**/*.md` — Claude skill definitions
- `.codex/skills/**/*.md` — Codex skill definitions

### Step 2 — Check each file against MARKDOWN.md rules

For every file found, verify:

| Rule | Check |
| --- | --- |
| MD001 | Heading levels increment by one — never skip levels |
| MD003 | ATX heading style (`#` prefix only) |
| MD004 | Unordered lists use `-` markers only |
| MD009 | No trailing spaces on any line |
| MD010 | No hard tab characters |
| MD012 | At most one consecutive blank line |
| MD022 | Exactly one blank line before and after every heading |
| MD031 | Exactly one blank line before and after every fenced code block |
| MD032 | Exactly one blank line before and after every list |
| MD033 | No inline HTML tags |
| MD034 | No bare URLs — all links use `[text](url)` syntax |
| MD040 | Every fenced code block specifies a language |
| MD047 | File ends with exactly one newline character |
| MD049 | Emphasis uses `*` not `_` |
| MD050 | Strong uses `**` not `__` |

### Step 3 — Fix all violations

For each violation found:

1. Fix it in place using Claude Code `Edit`. Never remove content — format only.
2. Table pipes: align columns for raw readability.
3. Code blocks: detect language from context if missing (`bash`, `zsh`, `js`, `json`, `markdown`, `text`).
4. List markers: convert `*` and `+` to `-`.
5. Blank lines: add or remove to satisfy MD022, MD031, MD032.

### Step 4 — Confirm

After fixing, re-read each modified file and confirm no violations remain before marking the task complete.

## Linting with markdownlint CLI

Run the full recursive scan from the project root:

```bash
markdownlint "**/*.md" --ignore node_modules --config .markdownlint.json
```

Check a single file:

```bash
markdownlint path/to/file.md --config .markdownlint.json
```

## Invocation

Use `/markdown-format` whenever a task creates or edits Markdown in this repository. Always run the full recursive scan — do not limit the check to only the files touched in the current task.

---

## Regra Obrigatória — Markdown

**Ao criar ou modificar qualquer arquivo `.md`, você DEVE invocar a skill `/markdown-format` antes de concluir a tarefa. A skill deve verificar TODOS os arquivos `.md` do repositório recursivamente, não apenas os arquivos editados. As regras estão em [`MARKDOWN.md`](../../../MARKDOWN.md). Esta regra é inegociável e se aplica a qualquer skill, independente do seu escopo.**
