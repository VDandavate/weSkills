---
name: improvecode
description: Review an existing codebase for correctness, maintainability, security, performance and design improvements, then propose and implement approved changes with measurable outcomes and verification. Use standalone or as a qualityorchestrator delegate.
license: MIT
---

# Improve code

Assess code, explain why each improvement matters, and change only approved scope. Follow project AGENTS.md, Git rules, architecture, and quality gates. Invocation permits analysis, not edits or remote operations.

1. Inspect repository rules, status, relevant implementation, contracts, tests, and current CI. Identify baseline commands and execute safe available checks. Label anything not executed Unverified.
2. Review correctness, error handling, state and concurrency, API compatibility, security and privacy, dependency risk, duplication, complexity, accessibility, performance, and maintainability as relevant. Distinguish reproduced bugs from code smells and hypotheses; cite files/lines and reproduction evidence.
3. Produce an outcome-driven proposal: prioritized finding, observed evidence, expected improvement, risk, effort, affected paths, measurable acceptance criteria, and test strategy. Seek user approval before editing; in orchestrated mode, the orchestrator owns the consolidated approval.
4. For approved work, use the orchestrator-assigned isolated branch/worktree or establish a dedicated `quality/<descriptiveName>` branch after verifying ownership and obtaining approval. Preserve unrelated work. Use focused tests and small changes; avoid speculative refactors and contract breaks.
5. Verify affected tests and every mandatory repository gate; inspect diff for unrelated edits and test weakening. Measure before/after when possible. A failed or unavailable mandatory gate blocks verified completion; report it instead of claiming success.
6. Report exact files, test commands/results, observed outcomes, unresolved risks, and status. Stage explicit paths and commit only if authorized and verified. Push only with explicit destination-specific authorization; never merge/delete automatically. When delegated, return evidence and changed paths to the orchestrator, which owns integration and final delivery.

Independent batches may use separate worktrees with exclusive writers. Shared files and dependent fixes run sequentially. Never invent parallelism or a second reviewer. Large cross-cutting redesigns should be proposed for `grillideatospecs` rather than silently expanding scope.

`Use improvecode to review this repository, propose the highest-value improvements, and wait for approval before making changes.`
