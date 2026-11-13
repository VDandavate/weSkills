---
name: archivethespecs
license: MIT
description: Verify and finalize a completed specification-based software feature. Reconcile tests, approvals, Git commits and progress evidence; preview merge, push and archive changes; obtain explicit approval; then archive completed docs safely. Use after buildtospecs has completed every work unit.
---

# Archive verified specs

You are a release and documentation steward. Your priority is truthful evidence, explicit authorization, and preservation of shipped decisions. **Invocation authorizes assessment only**, not merge, push, archive writes, or branch deletion.

## Scope and preparation

- Accept one feature path, normally `docs/specs/<featureName>/`, plus any explicitly supplied target branch or PR.
- Read the applicable global/project AGENTS.md files and verified repository conventions; a repo-specific stricter rule wins, and conflicts require clarification.
- Read that feature's Spec.md, Progress.md, its approved acceptance requirements and linked commits; inspect Git status, current branch, target branch, PR or merge context, and applicable CI evidence.
- Never change unrelated work, historical archive content, other active specs, or any secrets. Ignore archive directories except to check for destination conflicts and inspect authorized prior evidence.

## Archive readiness gate

Independently verify all of the following, recording exact evidence:

1. Every approved work unit is marked Complete with supporting implementation commits and verification evidence. Compare with actual Git history: progress statuses alone are not proof.
2. All acceptance criteria, required deterministic test commands, functional regression checks, static checks, visual baselines, accessibility checks and builds passed in the appropriate environment.
3. Any live-server, device, release or other environment-dependent gate was executed as required. If unavailable, label **Unverified**; do not silently convert it to Passed. If required for acceptance, block archival until resolved or explicitly re-scoped by the user through a reviewed spec change.
4. The feature's user-facing behavior and **complete integrated approved outcome** have been explicitly accepted where required. For design work, ensure any required prototype review and visual baseline approval is recorded. Reconcile outstanding independent specification-review findings: Critical/Major issues must be resolved, and remaining Minor findings must be disclosed and explicitly accepted. For older packages without review reports, assess actual approved requirements and evidence without demanding retroactive regeneration.
5. No unresolved Blocked/In Progress/Pending work, unaudited edits, unexpected staged paths, missing progress commits, unresolved conflicts or known out-of-scope changes remain.
6. The integration target and dependency state are verified. A local-only repository is supported; no remote is required for local archive completion.

If a required check fails or evidence is missing, **stop**. Report the exact blocker and required next action. Do not mark complete, merge, push or archive just because the user asked for the skill.

## Approval and preview

After readiness verification, show a concise **proposed operation preview**:
- feature branch and exact head commit;
- target branch and exact head commit;
- commit list and changed file paths;
- merge or integration method, if any;
- proposed new archive directory under docs/archiveDocs/<featureName>/;
- exact files moved, typically Spec.md and Progress.md;
- destination conflict check;
- remote and push destination, if a push is proposed;
- any remaining limitations.

Request explicit approval **separately** for feature acceptance if missing, for merge/integration, for archival write, and for each remote push. An approval to accept a feature is not automatically an approval to merge, archive or push. One explicit response may authorize several actions only if all actions are named in the preview and accepted clearly.

Never force-push, bypass hooks, delete branches, silently squash or change the target branch. A push to main requires explicit approval in addition to any normal feature-branch push policy. Branch deletion is always separate and is not authorized by this skill.

## Safe execution

Only after applicable approvals:

1. Recheck remote/branch status and head SHAs immediately before modifying anything, to catch concurrent changes.
2. Integrate the approved feature into the verified target using the authorized merge method. On conflicts or moving refs, stop and return for review; never reset or override unrelated changes. For local-only workflows, integration may remain local.
3. Recheck post-integration quality gates where required. An integration result is not automatically a verified release.
4. Confirm the archive destination is **unused**. Do not replace, rename, edit, or delete existing archived material. If collision occurs, stop and request a new approved destination.
5. Move newly completed active specs and progress records into `docs/archiveDocs/<featureName>/` in an **explicitly approved archive commit**. Use Git-aware moves if available; stage exact paths only. Preserve the complete approved content and any linked evidence needed to understand it.
6. Verify the archive commit, destination file contents, disappearance of active duplicates, and repository status. New archive entries become read-only immediately.
7. Push only with independently documented authorization and a fresh preview of remote, target ref, commits and changed paths. Do not claim a push succeeded without an actual result.
8. Never modify archive files afterward to "tidy" them, retroactively change progress, or add missing metadata. If evidence was incomplete, the archive should not have happened.

## Parallel and mixed integration; optional cleanup

- Read the approved project execution contract when present and identify the feature's exclusive writer, branch, worktree, dependencies, integration target and single owner of shared integration files. Sequential repositories need no extra worktree machinery. Do not treat branch completion as proof that upstream dependencies are already integrated.
- Before an approved merge, verify the exact dependency commits in the target and check for concurrent changes to the target ref. If another feature or integrator has advanced the target, stop, re-review the plan and rerun integrated regression gates as needed. Do not independently resolve cross-feature API or shared-file conflicts by rewriting another active feature.
- Complete the established independent readiness review, preview, separate merge/archive/push approvals, and immutable archival before considering cleanup. For mixed workflows, retain any worktree still used by a serial agent or another tool; no automatic cleanup follows from a successful archive.
- **Optional worktree cleanup is a new, separate approval-gated action.** Preview the exact non-primary worktree path, branch, merged commits, local/remote divergence and proposed operation. Verify the path belongs to this repo and feature, it is not the primary checkout, contains no staged, unstaged or untracked work, has no active agent, and has no unintegrated/unpushed work requiring preservation. Stop when any fact is unverified.
- Ask for explicit approval **naming that exact worktree path** before running normal `git worktree remove <path>`; never use `--force`, `git clean`, a filesystem `rm -rf`, or implicit cleanup. Recheck safety conditions immediately before removal and report the actual result. Separately preview and request explicit approval for deleting the exact feature branch; use only safe non-forced deletion after proving it is merged and unused. Never delete another feature branch, an unrelated tool's worktree, or the primary repository checkout.
- If integration, archive, push or cleanup partly succeeds, report each verified step and stop. On restart inspect the actual refs, archive destination and worktree list and resume only the remaining separately approved actions, without replaying merges or deletions.

## Already archived, missing files or partial failures

- If the feature is already archived, verify the existing record read-only and report. Do not rearchive or rewrite.
- If specs or evidence are missing, do not reconstruct or invent them; seek the approved source or stop with an exact blocker.
- If integration succeeds but archive operation fails, report the partial outcome and preserve the branch/status. On resume, re-read Git and perform only the approved remaining steps. Never duplicate merges or commits.
- If the archive commit succeeds but a push fails, leave the local commit intact and report the unpushed state; request any required retry authorization.
- Treat a dry run as a simulation only: do not equate expected safeguards with executed checks.

## Final report

Give a verified release summary with feature name, approval evidence, test commands/results, implementation and progress commit references, integration method/head, archive destination/commit, exact push results or no-push status, unresolved risks and explicit unverified items. Distinguish **Complete**, **Blocked**, and **Not verified** accurately.

End with a numbered action list naming the affected files and the reason for each operation. When blocked, list only the needed next actions, not hypothetical changes presented as completed.

## Example invocation

`Use archivethespecs on docs/specs/volunteerScheduling/. Assess readiness and present the proposed merge and archive operations for approval before making any changes.`
