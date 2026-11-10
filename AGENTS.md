# Global agent rules
These rules override default skill behavior and language style guides, including PEP 8.
A repo's own rule file may be stricter. Follow the stricter rule. If the two conflict, stop and ask.

## Naming (non-negotiable, all projects)
- No underscores in any identifier, file name or directory name we own.
- No UPPER_SNAKE_CASE anywhere. Constants use camelCase, marked immutable with the language's own feature where one exists.
- Variables, functions, methods, code files and directories: camelCase.
- Classes and types: PascalCase. A file that holds a class is still named in camelCase.
- Documents we author use PascalCase (Plan.md, Context.md, Decisions.md).
- Industry-standard names keep their expected spelling (README.md, AGENTS.md, SKILL.md, CONTRIBUTING.md, CHANGELOG.md, Makefile, package.json, tsconfig.json, .gitignore).
- JSON and YAML keys, enum and reason-code strings, and log tags we author are camelCase. Headings use plain words with no underscores.
- Hyphens are allowed only where an industry standard or tool requires or expects them: git branch names, URL slugs, CSS class names and custom properties, CLI flags, npm package names, skill and agent names. Identifiers in code stay camelCase.
- No leading-underscore privates. Privacy is by convention.
- Allowed exceptions, flagged in your report each time:
  1. Names the language requires (for example __init__, __main__).
  2. External names we do not own: environment variables, third-party API fields, database columns, framework parameters, and the keys and file names that tools define (package.json, docker-compose.yml, CI workflow files, pytest.ini, requirements files). Keep the exact spelling only inside a quoted string or the tool's own file, and read values into compliant variables.
- If a task seems to need any other exception, stop and ask. Do not decide alone.
- Legacy code: do not rename existing violations outside your task's scope. New and changed code must comply. Existing violations are cleaned up in dedicated sprints.
- Run the repo's naming check before claiming done. If none exists, say so.
- Never add entries to a baseline file to make a check pass. New violations fail the gate.

## Verification
- Run the repo's gate command before claiming done and report the exact result.
- State what you did not verify.
- Never weaken, skip or bypass a gate to make it pass.

## Scope and safety
- Stay inside the task scope. Do not touch other files or sibling work.
- Never read, print or commit secrets, .env files or real personal data.
- Stage named files only. Never use git add -A or git add .
- Do not commit, push, merge or delete branches unless asked. Invocation of `buildtospecs` explicitly authorizes creation/reuse of its feature branch and the documented specification-baseline, work-unit, and progress-tracking commits for the selected feature only. Invocation of `archivethespecs` authorizes assessment only; merge, archive write, and push still require explicit approval after a preview. No workflow invocation authorizes branch deletion.
- Before any push, show the remote, branch, commits and files. Pushes to feat/, fix/, docs/ and build/ branches may then proceed when specifically authorized by the workflow approval; pushes to main always wait for my explicit approval. Never infer push authorization from implementation-only requests.
- Never force-push. Never skip hooks with --no-verify.

## Working style
- At the start of work in any repo, use the project-standards skill if available. If unavailable, inspect applicable AGENTS.md files and verified repository conventions directly; this fallback is explicitly allowed. Never assume missing required project rules.
- If a rule conflicts with the task, stop and ask one specific question.
- If work is unfinished, say what is left and what you need. Do not stop silently.
- If a repo's expected rule files are missing from a fresh clone, stop and ask. An intentionally absent project-level AGENTS.md is permitted when there are no meaningful project-specific rules; do not infer intentional absence when evidence suggests the file should exist.
- Plain text, concise, short bullets, copy-ready. No em dashes.

## Asking and reporting
- Every question states the decision, why it matters now, and a recommended option marked (recommended).
- Reports and summaries end with a numbered action list. Each item names the exact file, the exact change, and the reason.

## Shell discipline
- Prefer the read, grep and edit tools over shell for file work.
- Keep each shell command single-purpose. Never chain destructive operations into one command; list every target, get a yes, then run one command per call.

## Archived documentation
- `docs/archiveDocs/` contains completed specs, progress trackers, and related docs for shipped work.
- `docs/archiveDocs/` is read-only archive material. Agents must not modify, create, or delete files in `docs/archiveDocs/` for future development, testing, or engineering efforts. Narrow exception: after verification and explicit user approval, `archivethespecs` may move newly completed feature directories from `docs/specs/` into unused paths under `docs/archiveDocs/` as part of finalization. It must not overwrite or change an existing archive entry. The newly archived files become read-only immediately after that operation.
- Use `docs/archiveDocs/` only as read-only reference outside the narrowly authorized archival operation above.

## Licensing
- This repository is licensed under the MIT License. Keep the root LICENSE file intact.
- When distributing copies or substantial portions of repository-authored skill instructions, templates, or documentation, include the MIT copyright and permission notice as required by LICENSE.
- Do not claim that MIT licensing applies to linked third-party content or code from other repositories. Respect upstream licenses.
- Do not change the repository license or copyright holder without explicit approval.
