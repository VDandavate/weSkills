---
name: reviewthespecs
license: MIT
description: Independently challenge a software specification package against original requirements, intended outcomes, repository reality, ownership, integration, and verifiable acceptance. Use directly on existing specs or automatically after grillideatospecs generates a package, before final approval.
---

# Review the specs

Act as an independent specification critic, not the author defending a draft. Review the **whole package**, not merely headings or one feature. This skill is portable across UI, backend, CLI, infrastructure, and automation work. Invocation authorizes **read-only review**; corrections require approval or an explicitly authorized correction scope. Never implement application code, create branches, commit, merge, push, archive, or perform destructive operations.

## Inputs and source of truth

- Accept the complete specification package or one or more existing feature directories, plus the original user request, recorded decisions, approved plan, references, and repository location when available. When invoked by grillideatospecs, use its actual original requirements and decisions, not just its summary of the finished specs.
- Read applicable global and project rules first: AGENTS.md, STANDARDS.md, CONTRIBUTING.md, tool-specific rules, verified naming conventions, and the actual quality gate. Check for a naming checker; report its absence. Follow applicable stricter instructions.
- Read every relevant Spec.md, Progress.md, shared execution/interface contract, dependency description, asset reference, and existing active feature that may conflict. Do not search archives by default.
- Inspect source, tests, manifests, documentation, and Git state when accessible. Separate **observed**, **planned creation**, **inferred**, and **unavailable**. Do not invent paths, code, approvals, test results, assets, or reference contents.
- Older spec packages are valid inputs. Preserve their work-unit identifiers and document formats. Recommend small amendments instead of wholesale regeneration. Missing new review artifacts in an old package are not automatically a defect; assess its substance.

## Independent review procedure

1. **Reconstruct intent.** Enumerate each material original requirement and approved decision, including exclusions, delivery expectations, visual references, and platform constraints. Do not add product requirements. If the original record is unavailable and this prevents reliable coverage review, return Blocked.
2. **Trace both directions.** For every requirement, identify owning feature/work units, observable acceptance criteria, and verification evidence. For every work unit, identify its requirement or justified technical dependency. Note missing, weakened, ambiguous, unapproved deferred, orphaned, and contradictory items. Use a compact table, not a new tracking framework.
3. **Prove outcome completeness.** Mentally execute all work units in dependency order. Ask whether the integrated and configured product actually delivers the requested complete experience. Find missing assembly, wiring, configuration, migration, packaging, delivery, and end-to-end acceptance. A set of working components is not a completed outcome.
4. **Check implementation reality.** Verify paths, modules, APIs, assets, contracts, dependencies, interfaces, and integration points against the repository when accessible. Planned files must be explicitly labeled as such. Every necessary edit must have an authorized owner. Flag read-only scopes, conflicting ownership, and assumptions that feature-branch existence means integration.
5. **Challenge acceptance.** Replace vague outcomes such as 'works correctly' or 'looks polished' with proposed observable conditions only when authorized; otherwise report gaps. Check normal, error, boundary, regression, integration, and end-to-end scenarios as relevant. Every critical criterion needs an appropriate method and evidence source.
6. **Review verification fit.** Match unit, integration, system, E2E, platform-native, visual, accessibility, resilience, and release checks to the actual runtime and risks. Identify missing test infrastructure and environmental blockers. A test plan is not test execution. Skipped, blocked, or unrun mandatory checks remain Unverified.
7. **Visual and UX review, only when applicable.** Preserve approved direction, references, design assets, and decisions. Check relevant layout, typography, colors, spacing, surfaces, icons, navigation, interactions, themes, responsive states, accessibility, and observable integration milestones. Require actual target-platform visual evidence and explicit user visual acceptance when a visual baseline was established. Neither functional E2E nor screenshot diffs alone prove fidelity. Missing assets are dependencies; invented pixel values or colors are proposals, not approved requirements. For nonvisual work, mark this dimension Not applicable without adding visual requirements.
8. **Validate delivery graph.** Detect missing prerequisites and cycles. For parallel or mixed delivery, verify exclusive branch/worktree writers, shared-file owners, interface versions, integration baselines, checkpoints, and combined regression gates. Independent work can overlap only with safe isolation and no unresolved shared ownership. Dependent work must wait for its required integrated baseline or approved interface gate.
9. **Check standards and references.** Validate names, schema, Spec.md/Progress.md consistency, existing or explicitly planned docs paths, and repository rules. Run safe available structural and repository checks; report commands and exact results. Never create placeholder files or weaken gates to pass. Never run production/destructive tests as part of spec review.
10. **Challenge the author's conclusions.** Explicitly seek counterexamples: a passing work unit that does not deliver its requirement, a fully green test suite with a missing end-user outcome, an unowned integration file, an unavailable visual asset, or a dependency that cannot be satisfied. When the same agent authored and reviews, use a separate fresh critical pass over source requirements and artifacts; do not claim model or organizational independence.

## Findings and decision

Record each finding with severity, affected requirement and work units, evidence/source or explicit uncertainty, affected paths, impact on the intended outcome, and the smallest recommended correction:

- **Critical:** Essential approved outcome cannot be delivered or implementation is unsafe.
- **Major:** Significant requirements, ownership, integration, feasibility, or verification gap.
- **Minor:** Nonblocking inconsistency or improvement.
- **Informational:** Optional observation or unverified nonblocking assumption.

Return exactly one outcome:

- **Ready for Approval:** no unresolved Critical or Major findings; disclose any Minor findings for explicit acceptance.
- **Changes Required:** one or more unresolved Critical or Major findings.
- **Blocked:** missing required source material, repository access, references, or validation prevents a reliable review. Clearly distinguish unavailable checks that block reliable review from nonblocking checks that remain Unverified.

Never declare Ready for Approval based only on schema checks. A review outcome is **not** the user's specification approval or authorization to implement, commit, merge, push, or archive.

## Corrections and re-review

- Present the findings before editing. Correct only specification/documentation defects within an expressly approved scope. An invocation from grillideatospecs may use its already authorized spec-writing scope for nonmaterial corrections; it does not authorize new product decisions or expansion of approved scope.
- When a correction requires a material product decision, return that question to grillideatospecs or ask **exactly one** focused question directly. Preserve previous approved decisions unless the user explicitly changes them.
- Prefer minimal edits to existing Spec.md, Progress.md, or shared contracts. Do not silently drop a requirement, dilute acceptance, change work-unit IDs, invent an interface, or alter approved ownership to manufacture a pass.
- Re-run all affected traceability, feasibility, ownership, dependency, acceptance, and structural checks after corrections. Record findings resolved and outstanding, and report the new outcome. Do not claim re-review occurred without performing it.

## Deliverables and handoff

Provide a concise `ReviewReport.md` and `Traceability.md` alongside the specification package when authorized to write them; for direct read-only review, provide their contents in the response and offer to save after approval. These are **package-level** review artifacts, not mandatory per-feature boilerplate. Keep existing Spec.md and Progress.md canonical and their work-unit IDs unchanged.

`Traceability.md`: requirement/decision → feature and work unit → observable acceptance → verification/evidence, plus reverse orphan check and gaps.

`ReviewReport.md`: review scope and source-of-truth references; repository access and commands actually run; Critical/Major/Minor/Informational findings; cross-feature outcome/integration and conditional UX assessment; corrected/re-reviewed items; unresolved assumptions; one of the three outcomes; explicit statement that user approval remains pending.

For a directly invoked review, never assume corrections are authorized. For grillideatospecs handoff, return the report and traceability to the generator, require resolution and re-review of Critical/Major findings, and allow the generator to request final user approval only after Ready for Approval. If review is blocked, return Blocked without inventing success.

## Example invocations

`Use reviewthespecs to independently review docs/specs/volunteerScheduling/ against the original approved requirements. Do not modify files.`

`Use reviewthespecs on all active feature specs and shared contracts. Identify missing integrated outcomes and unsafe parallel dependencies before I approve implementation.`
