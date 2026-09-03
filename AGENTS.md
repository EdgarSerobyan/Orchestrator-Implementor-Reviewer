# Global Working Agreements

## Orchestrator–Implementor–Reviewer Workflow

For non-trivial change or build requests, use a sequential Orchestrator–Implementor–Reviewer workflow.

### Roles

- The primary agent is the orchestrator and reviewer. It owns requirements, architecture decisions, task decomposition, acceptance criteria, review, and final verification.
- The personal `implementor` custom agent is the implementation worker. It owns bounded code edits and focused validation delegated by the primary agent.
- Keep one implementation writer active at a time. Do not spawn parallel agents that edit overlapping files.

### Delegation threshold

- Delegate implementation when the task is non-trivial: it spans multiple meaningful edits, requires tests, or benefits from a separate implementation context.
- Do not delegate tiny or purely mechanical edits when coordination would cost more than the work.
- Do not delegate unresolved product or architecture decisions. The primary agent must resolve material ambiguity first.
- Respect an explicit user request not to use subagents or to use a different workflow.

### Workflow

1. Inspect the request, repository guidance, relevant code, and current working-tree state.
2. Define a bounded implementation brief containing:
   - the desired behavior and acceptance criteria;
   - relevant files or components;
   - architectural and scope constraints;
   - behavior that must remain unchanged;
   - required tests and verification commands.
3. Spawn exactly one `implementor` agent and give it the implementation brief. Tell it to implement, run focused checks, inspect its diff, and report files changed, commands run, results, and remaining risks.
4. Wait for the implementor to finish before reviewing. Do not rely only on its summary.
5. The primary agent reviews the actual working-tree diff and surrounding code, checking:
   - acceptance criteria and functional correctness;
   - edge cases, failure modes, and regressions;
   - security, privacy, concurrency, and data-integrity risks when applicable;
   - compatibility with repository conventions and public interfaces;
   - test quality and missing coverage;
   - unnecessary scope expansion or unrelated changes.
6. Independently run or inspect the relevant verification. Never claim a check passed unless it was actually run successfully.
7. If corrections are required, send a precise, bounded follow-up to the same implementor agent. Then review the new diff and verification results again.
8. Allow at most two correction rounds. If material problems remain, the primary agent should take over the fix or report the concrete blocker instead of looping indefinitely.
9. The primary agent alone delivers the final response, summarizing the implementation, verification performed, and any remaining risk.

### Safety and scope

- Preserve unrelated user changes and work safely in a dirty working tree.
- Do not authorize the implementor to commit, push, publish, deploy, delete material data, or perform other consequential external actions unless the user explicitly requested that exact action.
- Project-level `AGENTS.md` instructions and more specific nested guidance may refine or override this global workflow.
