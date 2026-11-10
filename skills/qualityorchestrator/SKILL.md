---
name: qualityorchestrator
description: Coordinate evidence-based code review, comprehensive testing, approval-gated dependency-aware remediation, independent verification, and safe branch delivery for an existing software repository. Use for holistic quality assessments and approved improvements.
license: MIT
---

# Quality orchestrator

Own the outcome and coordination, not the implementation of every check. Reuse `improvecode` and `testthoroughly` when available; otherwise follow their documented contracts directly and disclose the limitation. No separate orchestration service is required.

## Contract and safety

- Start by locating repository root, applicable AGENTS.md and other rule files, Git branch/status/worktrees, architecture, test commands, and current CI. Project-specific stricter rules win. Never assume a missing skill or tool executed.
- **Invocation authorizes assessment only.** Do not modify production code, tests, configs, Git refs, or remote state before explicit approval. A read-only assessment may run nondestructive tests if permitted by repository rules; warn first if tests can write data, use external services, or incur costs.
- For approved implementation, create/reuse a dedicated `quality/<descriptiveName>` branch, preferably in a separate Git worktree. Verify branch/worktree ownership, clean base and target ref. Never overwrite dirty or unrelated work. If workspace isolation is unavailable, request a safe checkout rather than pretending it exists.
- No push, merge, branch deletion, force operation, destructive test, or cleanup without the corresponding authorization. Proposal approval is not automatically push approval. The user may explicitly authorize a named push as part of the approved plan, provided the remote, branch, and scope remain unchanged; re-preview before acting.
- Never bypass hooks, lower quality thresholds, suppress findings, delete failing tests, stage wildcard paths, or expose secrets. Never make production-destructive test calls.

## Workflow

1. **Discover and baseline.** Inspect relevant code and architecture; determine language-specific gates, tests, CI, dependencies, trust boundaries, runtime and release requirements. Execute safe available checks and record exact commands, exit codes and environments. Distinguish pre-existing failures from introduced regressions. A repository/API-only dry run is *not* test execution.
2. **Independent assessments.** Request a code assessment from `improvecode` and a test assessment from `testthoroughly` where available. These may run concurrently on read-only snapshots; otherwise sequentially. Review correctness, contracts, maintainability, security, supply chain, privacy, accessibility, performance, deployment, and recovery based on risk. Use evidence tiers: Confirmed (reproduced), Configured (directly inspected), Suspected (reasoned), Unverified (not tested).
3. **Outcome-driven proposal.** Deduplicate findings; show baseline evidence, impact, priority, confidence, expected measurable improvement, tests, risk, cost, and scope. Group remediation into dependency-aware batches. Identify files/owners, shared-file conflicts, prerequisites, required approvals, and integration order. Prefer meaningful outcomes over cosmetic churn. Clearly mark proposed, not completed, benefits.
4. **Approval checkpoint.** Present the plan and wait. Allow the user to approve a subset, revise, defer, or cancel. New material scope or risk requires renewed approval. Specify any requested authorization for local commits and a named remote push separately.
5. **Execute approved batches.** Use the isolated quality branch. Parallelize only truly independent batches with exclusive writers/worktrees and non-overlapping files; dependent or shared-file changes are sequential. If multi-agent/worktree support is missing, use sequential execution with identical gates. Establish meaningful regression tests where practical; implement the smallest fix. Preserve contracts and unrelated changes. Limit repair loops and stop on diminishing returns or unresolved blockers.
6. **Integrate and verify.** Review each batch and test it before integration. Reconcile branch heads and conflicts safely; rerun full mandatory gates on the combined result, including affected unit/integration/E2E, security and platform checks. Prefer a genuinely independent review/test pass. Do not treat an implementing agent's statement as test evidence. Record unavailable environment-dependent checks as Unverified; a required unverified or failed gate blocks a verified-complete claim.
7. **Outcome-driven result.** Compare measured before/after behavior, defects fixed, tests added, regressions, remaining risks, scope changes, exact checks/results, and confidence. Separate confirmed results from expectations and unknowns.
8. **Git delivery.** Only after required checks pass and authorization is in place: stage explicit paths, inspect diff, commit verified changes, verify commit SHA, preview remote/branch/ref, and push only if specifically authorized. If required checks fail, stop and report the blocked branch without presenting it as verified. Never merge or discard automatically; user chooses.

## Quality gates

Always: repository instructions; safe baseline; requirements/contracts; meaningful tests; security/privacy; scope and Git integrity; independent review where feasible; honest evidence. Risk-based: integration/E2E, exploratory constructive and negative cases, resilience, accessibility, performance, dependency/license review, Rust/native gates, packaging and release smoke tests. Never skip a mandatory project gate because it is labeled risk-based here.

## Recovery and reporting

On interruption, re-read actual Git refs, status, worktrees, approvals, batch ownership and verification artifacts before resuming. Do not assume a prior agent completed a batch. If there is no durable progress ledger, reconstruct state from Git and test evidence; create minimal tracking only when needed.

Reports must include: scope and branch; findings with evidence tier; approved versus deferred batches; exact commands and results; before/after outcomes; unresolved failures and Unverified checks; changed paths; commit SHA and push result (or explicitly none); next approval/action. Never claim full code review, comprehensive E2E, or production readiness based only on manifests and README files.

## Invocation

`Use qualityorchestrator to assess this repository. Run safe baseline checks, produce an outcome-driven proposal, and wait for my approval before changing code. Use a dedicated quality branch for approved remediation.`
