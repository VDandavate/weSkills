# Global agent rules

Apply these defaults across projects. Follow applicable repository instructions and explicit task requirements. Project rules may add stricter constraints, but must not silently weaken these safeguards. If rules genuinely conflict, ask one focused question before acting. Prefer simple, maintainable solutions and minimal changes.

## Naming
- For names we control: camelCase for variables, functions, methods, code files, directories, JSON/YAML keys, enum values, reason codes, and log tags; PascalCase for classes, types, and authored Markdown documents (for example `Spec.md` and `Progress.md`).
- Use camelCase for constants with language-supported immutability; do not introduce UPPER_SNAKE_CASE, leading-underscore private names, or underscores in names we control.
- Preserve required names from languages, tools, frameworks, protocols, third-party APIs, environment variables, and industry-standard files (for example `AGENTS.md`, `README.md`, `SKILL.md`, `package.json`, `.gitignore`, and Python dunder methods). Preserve their exact spelling at integration boundaries; do not rename external contracts merely for style.
- Hyphens are permitted where expected by tools or established conventions, including Git branches, skill names, URLs, CLI flags, CSS, and package names.
- Do not rename unrelated legacy code to satisfy naming preferences. Record any required naming exception and its reason. Ask before inventing a new exception.
- Run the repository's naming check when available. Do not weaken checks or expand baselines to conceal violations.

## Before work
- Identify the repository root, applicable instruction files, current branch, and relevant existing code before editing.
- Start every coding, review, planning or cleanup task by finding the repo's rule files: AGENTS.md, STANDARDS.md, CONTRIBUTING.md, CLAUDE.md, .cursorrules, .windsurfrules, docs standards. Find the gate command: AGENTS.md first, then a Makefile target named `check`, then package.json scripts (check, test, lint, namingLinter). If none exists, say so in your report.
- Find the naming checker. If none exists, say so. Never claim naming compliance without running one. If the repo expects a file that is missing (for example a gitignored privateDocs folder), stop and ask rather than inventing rules.
- Keep project-wide architecture, commands, and conventions in project-level instructions when useful. Keep feature-specific requirements in specifications and repeatable procedures in skills. Do not duplicate instructions unnecessarily.
- Resolve material uncertainty with one question at a time: state the decision, why it matters, options where useful, and mark the recommendation `(recommended)`.

## Implementation and verification
- Change only what the task requires. Preserve unrelated work and avoid speculative features, unnecessary dependencies, or unrelated refactoring.
- Follow existing architecture and coding conventions unless an approved task requires change. Prefer small, cohesive, testable increments and pragmatic TDD for testable behavior.
- Review changes for correctness, regressions, security, maintainability, and unintended scope before declaring completion.
- Run applicable tests, naming checks, and repository quality gates. Report the exact commands and results. If a check cannot run, state why and what remains unverified; never imply a check passed when it did not.
- Never bypass checks, skip Git hooks, or change baseline files just to obtain a passing result.
- Report in this shape: files changed; gate command and exact result line; naming exceptions used, if any; what you did not verify; open questions.
- Consider work done only when: the gate passed with the exact result line; the naming check shows zero new violations for the changed code; the staged file list matches the task; docs or spec are updated if behavior changed.

## Data and command safety
- Do not read, expose, or commit secrets, credential files, `.env` contents, or real personal data unless the user explicitly authorizes an essential, safe operation. Never print secret values. Use redacted examples.
- Prefer targeted read/search/edit tools for file work. Inspect targets before destructive actions; obtain explicit approval for destructive or irreversible operations. Do not bundle destructive shell operations.
- Never overwrite or discard unrelated edits. When ownership of changes is unclear, pause and ask.

## Git authorization
- Inspect branch, staged/unstaged changes, and untracked files before committing. Stage explicit named paths or hunks only; never use `git add -A` or `git add .`.
- Do not commit, merge, push, reset, or delete branches without authorization. Invoking `buildtospecs` authorizes only its documented specification-baseline, work-unit, and progress commits on the selected feature branch; it does not authorize pushing or merging.
- Invoking `archivethespecs` authorizes inspection only. Obtain explicit approval after showing the intended target, remote, commits, files, and actions before merging, archiving, or pushing. Pushes to `main` always require explicit approval.
- Never force-push, rewrite shared history without approval, bypass hooks with `--no-verify`, or delete branches without a separate explicit request.

## Concurrent feature execution
- Support sequential, parallel, and mixed execution. Sequential use must not require multiple worktrees; concurrent feature writers must use separate branches and worktrees, with one writer per feature and `Progress.md`.
- Discover actual repository worktrees, branches, owners and shared baseline before starting. Reuse the assigned checkout when it matches; never silently change the current tool workspace, move another agent, or create a conflicting worktree. Stop if branch ownership, an occupied path, or uncommitted work is unclear.
- Honor feature prerequisites and reviewed shared interfaces. Independent work may proceed concurrently; dependent integration waits for the required upstream merge. Do not invent interface contracts or let concurrent agents independently edit shared integration files.
- Approval to plan or build is not approval to merge, push, archive, delete a branch, or remove a worktree. Cleanup requires separate approval of each exact worktree/branch, after verifying it is no longer used, fully integrated, clean (including untracked files), and not the primary checkout. No force removal.

## Completed specifications
- `docs/archiveDocs/` holds completed specifications as read-only history, not active implementation instructions. Exclude it from routine agent discovery and modifications; any search exclusion is not a security boundary.
- After verification and explicit approval, `archivethespecs` may move a newly completed feature directory from `docs/specs/` to an unused location in `docs/archiveDocs/`. Never overwrite or modify an existing archive entry. The new entry becomes read-only after archival.

## Communication
- Write plainly and concisely. Use short sentences, clear headings, and copy-ready output. Avoid em dashes and inflated language.
- State what changed, what was verified, what was not verified, and any blockers or remaining work. Do not claim success prematurely.
- End implementation reports with a short numbered next-action list identifying specific files, changes, and reasons, when actions remain. Do not invent actions merely to satisfy the format.
