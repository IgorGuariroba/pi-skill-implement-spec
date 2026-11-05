---
name: implement-spec
description: Implement a spec and its ticket graph on one integration branch using
  Pi workers.
disable-model-invocation: true
license: MIT
metadata:
  author: Matt Pocock
  adapted_by: Igor Guariroba
  version: 1.0.0
---


# Implement spec

Implement the provided spec and tickets on one **integration branch**. Tickets form a **task graph**: the **frontier** contains only tickets whose dependencies have been integrated and validated.

Read `references/pi-workers.md` before delegating. Workers are fresh Pi processes, not native subagents. Share absolute context pointers to the spec, tickets, exploration notes and commits. Keep notes and execution artifacts outside the repository.

## Steps

1. **Map the graph.** Read the spec and every ticket; record acceptance criteria, dependencies and tracker workflow. Use `docs/agents/issue-tracker.md` when present, otherwise the relevant installed tracker skill. Ask for any missing spec, tickets or tracker information that blocks execution. This step is complete when every ticket is accounted for and the graph has no unresolved dependency ambiguity or cycles.

2. **Explore when needed.** Use a read-only exploration worker for unresolved codebase/documentation questions. Have it return evidence and pointers; the coordinator saves useful notes outside the repo. Exploration is complete when each blocking question has an answer or an explicit blocker.

3. **Prepare integration.** Record the starting SHA and existing local changes, then create the integration branch without disturbing them. The coordinator is its sole writer and performs merges serially. If the tracker closes work through PRs, or the user requests one, open a draft after the first integrated commit; reference the spec and tickets using the tracker's closing convention.

4. **Dispatch the frontier.** Create a dedicated branch/worktree from the current integration tip for each ready ticket, then start a fresh implementer worker there. The prompt must require the worker to:
   - confirm its worktree, branch and base SHA before editing; report a mismatch to the coordinator rather than resetting;
   - read `../tdd/SKILL.md` (pass an absolute path) and implement the ticket's acceptance criteria;
   - run relevant checks, commit only its own work and report commit SHA(s), acceptance evidence, checks/results and blockers;
   - leave integration and other workers' worktrees to the coordinator.

   Start independent tickets concurrently through the shared worker guide. A ticket is ready for integration only after the coordinator verifies its commit(s), report and clean worktree.

5. **Integrate serially.** Merge each completed ticket into integration. If the tip advanced, resolve conflicts and validate the combined state before accepting it. Delegate conflict resolution only to a fresh worker with exclusive ownership of the integration worktree while the coordinator pauses writes. Unresolved conflicts or failed checks keep the ticket blocked. Recompute the frontier only after a successful merge and relevant integration checks; return to step 4 until every ticket is integrated.

6. **Review the whole spec.** Read `../code-review/SKILL.md` and review integration against the starting SHA from step 3. Supply the spec and all ticket criteria. Fix actionable findings in a fresh implementer worktree and integrate serially. Run the full validation suite and re-review affected areas. This step is complete when every criterion has evidence, both review axes have results (or an explicit unavailable source), and outstanding issues are resolved or reported as blockers.

7. **Deliver and clean up.** Only after validation, mark the draft PR ready, or resolve tickets using the tracker's workflow when no PR exists. Do not mark incomplete work resolved. Report integration branch, commits/PR, checks and ticket outcomes. Remove only worktrees created by this run that are clean and whose commits are integrated; preserve blocked/unmerged work and execution artifacts for recovery. Avoid forced cleanup.
