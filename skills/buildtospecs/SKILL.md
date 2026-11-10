---
name: buildtospecs
license: MIT
description: Implement exactly one approved feature specification with pragmatic test-driven development, strict repository quality gates, sequential verifiable work units, safe Git commits, progress tracking and reliable resume. Use when asked to build docs/specs/<featureName>/Spec.md.
---

# Build to specs

You are a careful senior engineer. Execute **one approved feature** from its own Spec.md and Progress.md. Never use this skill to invent a missing specification or silently expand scope. Work units are sequential; independently buildable features may run in separate branches and Git worktrees.

## Inputs and boundaries

- Accept a feature directory such as `docs/specs/exampleFeature/` or a precise feature name. Confirm the actual repo, target branch, files, work-unit IDs and dependencies.
- Read applicable global and project AGENTS.md rules and verified project conventions. Stop for unresolved conflicts or unexpectedly missing required rules.
- Inspect architecture, manifests, relevant source, tests, Git status, open changes and the active feature specification. Ignore archived docs in routine discovery.
- The command to invoke this skill authorizes **only** the selected feature's branch/worktree creation or reuse and its planned spec-baseline, implementation-unit and progress commits, subject to stricter local rules. It does **not** authorize push, merge, archive writes, force operations, or branch deletion.
- If repository or test execution is unavailable, use a clearly labeled **dry run** only when the user explicitly requests one. Never claim simulated results are verified.

## Delivery mode and worktree assignment

- Read any **approved project-specific parallel-execution contract** referenced by the selected `Spec.md`; determine whether the project operates in `sequential`, `parallel`, or `mixed` mode. If no contract exists, keep the original single-feature workflow; never invent an assignment or require parallel infrastructure.
- In sequential mode, use an appropriately isolated current checkout and the selected feature branch; do **not** require a new Git worktree merely to execute the next feature. In parallel/mixed mode, each concurrently active feature must have one exclusive writer, branch, worktree and progress ledger. Different tools must never operate concurrently in the same checkout or write the same `Progress.md`.
- Inspect `git worktree list --porcelain`, `git status --short`, `git branch --show-current`, the target branch SHA and any project assignment before modifying anything. Verify actual repo identity, branch, physical path and absence of conflicting users. Existing assigned worktrees must be reused, not recreated. If the branch is checked out elsewhere, the path is occupied, or ownership is uncertain, **stop** rather than move/delete/reassign anything.
- When a new worktree is required and creation is authorized under this skill and any stricter project rule, verify the approved integration baseline contains the approved feature specs, then create the assigned feature branch/worktree without overwriting an existing path. Check the resulting branch, worktree mapping and files. Some agent tools cannot switch workspace automatically: report the required folder and **stop edits** until the agent is actually running in that folder.
- For mixed delivery, transfer a serial agent to its next branch only after its previous checkout is clean, its handoff is verified, and no concurrent writer owns that checkout. Never reinterpret shared or untracked files as disposable.
- Work-unit prerequisites and approved interface versions control eligibility. Independent code may be written concurrently in distinct owned files; dependent production wiring must stop until upstream integration/contract gates are satisfied. A separately reviewed interface enables bounded work, not a claim that an upstream feature has been integrated.
- Treat shared integration files as single-owner paths unless a reviewed agreement names a safe alternative. Record owner/consumer/API version, upstream SHA and acceptance tests in the feature evidence; do not rewrite another agent's contracts or silently stack feature branches.
- On restart, re-verify ownership, upstream refs, branch, worktree and ledger before reconciling the incomplete unit. Follow original Red → Green → Refactor, gating and separated-commit rules unchanged. A specification-only or no-code dry run does not establish that the required application tests passed.

## Preflight and reconciliation

1. Confirm Spec.md and Progress.md are present, parseable, consistent and approved. Check non-overlapping work units, prerequisites, acceptance criteria and verifiable tests.
2. Check current branch, status, worktree ownership, staged paths, Git log and remotes. Never overwrite existing dirty work, change other feature branches or reset/stash without specific consent.
3. Enforce a **single feature per invocation**: normally create or reuse feature/<featureName>, from the approved integration target. A separate worktree is allowed for independent features; never have concurrent agents write one Progress.md or branch.
4. Compare Progress.md with actual commits and files. A marked Complete unit is not trusted without evidence; an implementation commit is not proof of passing tests. Resolve discrepancies before continuing.
5. Confirm feature dependencies were integrated in the chosen target before beginning; do not silently build stacked feature branches.
6. Verify baseline requirements, including regression coverage for code about to change, current test failures, version/data migration constraints, and any mandatory design review gate.
7. If spec is materially incomplete or incompatible with verified code, stop and ask **one highest-priority clarification**, with a recommendation. Do not invent missing acceptance conditions.

## Baseline commit

- If approved specs are not tracked on the feature branch, stage **only** named Spec.md and Progress.md files and make a distinct spec-baseline commit. Never add unrelated or sensitive files.
- If baseline is already committed, verify its contents and avoid duplicate commits.
- Record branch and baseline commit in the progress tracker when appropriate, without fabricating a hash.

## Execute one unit at a time

Select the earliest eligible work unit whose prerequisites are satisfied. For each unit:

1. Set the unit to In Progress in Progress.md using the established ledger format. Preserve any prior evidence.
2. Identify exact owned code/test paths, expected behavior, existing behavior, and applicable acceptance criteria. Do not rewrite unrelated code.
3. Add a failing test first where behavior can reasonably be tested: **Red → Green → Refactor**. For visual or exploratory tasks that cannot be TDD-first, record the reason and establish reproducible verification before implementation.
4. Implement the smallest maintainable change, following project naming, security, compatibility and architecture rules.
5. Run the feature's tests **and the complete required deterministic repository gate**: naming, docs, type checks, unit, integration, UI/E2E, accessibility, visual and build checks as applicable. Run live-environment checks when available and required. Never call unrun or unavailable tests Passed.
6. If a mandatory check fails, investigate and record precise command, failure, context and evidence. Fix feature-caused failures. Unrelated fixes require separately approved scope; if required checks remain failing, mark Blocked and stop. Do not weaken checks.
7. If an external approval milestone applies (such as a UI prototype), present the artifact and request explicit approval. Passing tests never substitutes for human approval.
8. When all acceptance criteria and mandatory gates pass, stage **explicit implementation/test paths only**, create **one implementation commit for this work unit**, and verify the actual SHA.
9. Update Progress.md with Complete, tests/commands/results, the implementation SHA, and any approved deviations. Commit **the progress document separately**. Verify the progress commit SHA from Git after creation. A commit cannot record its own SHA in its own content.
10. Advance only after confirming both commits and requirements. If no implementation change is needed because behavior already exists, document verifiable evidence and obtain approval for a no-op unit rather than fabricating a code commit.

## Resume safely

- On restart, re-read Spec.md, Progress.md, Git status/log, tests and any approved decision record. Do not trust a stale conversation summary over repository state.
- Recognize crash windows: before implementation commit; after implementation commit but before progress commit; or after progress commit. Reconcile rather than duplicating code or commits.
- Exactly four persisted unit statuses: **Pending, In Progress, Blocked, Complete**. "Interrupted" and "Reconciled" are events in notes, not extra statuses.
- Preserve partial changes. Never claim recovery automatically repaired work that was not verified.
- A Progress.md entry may cite the implementation commit and test evidence; the progress commit's SHA is verified from Git and can be reported externally or in a later commit, not self-referentially stored in the same commit.

## Quality and safety

- Existing user data, functionality, interface contracts and migrations must be preserved unless the approved spec explicitly changes them.
- Use deterministic mocks for routine LLM/UI testing when relevant, and a separate real-integration gate where appropriate.
- Respect naming constraints and repository checks. Do not add exclusions to make failures pass.
- Never stage wildcard paths; never force push; never bypass hooks. Never read or commit secrets, local environment files, or real personal data.
- If an approval or required execution environment is missing, mark Blocked or leave the existing status with a precise note. Do not silently proceed.
- Do not push or merge. If the user separately requests a push, preview remote, branch, commits and changed paths and request explicit authorization according to the applicable AGENTS.md.

## Completion and handoff

Before marking a feature complete, confirm every unit, acceptance criterion, test gate, approval and Git record. Do not archive completed docs here: that belongs to archivethespecs.

Report the feature, branch, current unit status, exact commands and outcomes, all unverified checks, implementation/progress commit SHAs, risks, and the next action. End with a concise numbered action list identifying files changed and why. If blocked, state the blocker and how to resume.

## Example invocation

`Use buildtospecs for docs/specs/volunteerScheduling/. Start with the first eligible unit, preserve existing work and run the required repository gates.`
