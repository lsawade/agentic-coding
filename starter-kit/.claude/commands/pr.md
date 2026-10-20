---
description: Prepare a pull request for this project
---
Prepare this change for human review. Do not open the PR.

1. Run the test command from CLAUDE.md and show the output (pass and fail counts, and any failure messages).
2. Summarize the change in three lines or fewer.
3. List every file touched, one per line, with a few words on what changed.
4. List the assumptions the change makes.
5. State what was NOT tested.
6. Write the PR description to `pr-draft.md` with sections: Summary, Files, Assumptions, Not tested, How to verify. If any test failed, say so at the top of `pr-draft.md`.
7. Stop. The human reads the diff and opens the PR.

Do not commit, push, or run `gh pr create`.
