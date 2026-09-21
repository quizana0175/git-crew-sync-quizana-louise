Git Crew Sync Lab Workflow & Analysis
Student Name: Louise Daniella Quizana
Repository: git-crew-sync-quizana-louise
Date: September 21, 2026

Task 1: Push a Change from Clone A
Branch: feature/overtime-pay
Objective: Add overtime pay for shifts exceeding 8 hours (time-and-a-half rate).
Implementation: Updated calculatePay in shifts.js to compute regular pay for the first 8 hours and 1.5× rate for hours beyond 8. Added test coverage in test.js.
Commit: Add overtime pay for shifts over 8 hours - quizana.louise
Task 1 Evidence
<img width="1912" height="1079" alt="Screenshot 2026-09-21 210423" src="https://github.com/user-attachments/assets/f124053c-39cb-4772-bb63-76446cbc3e86" />

Task 2: Diverge from Clone B and Encounter Rejected Push
Branch: feature/overtime-pay
Objective: Modify the same function (calculatePay) in Clone B without fetching Clone A's push to intentionally diverge branches. Changed truncation (Math.floor) to rounding (Math.round).
Commit: Round shift pay instead of truncating - quizana.louise
Push Result: The push was rejected (! [rejected] feature/overtime-pay -> feature/overtime-pay (fetch first)).
Task 2 Evidence
<img width="1918" height="1079" alt="Screenshot 2026-09-21 210725" src="https://github.com/user-attachments/assets/17ccf3d8-8170-46fd-ab4e-3d9aad5b38e1" />


Task 3: Reconcile Divergence with a Merge
Branch: feature/overtime-pay
Objective: Fetch and merge remote changes from Clone A into Clone B.
Resolution: Resolved the merge conflict in shifts.js so that both behaviors survive: overtime pay for shifts over 8 hours AND rounding (Math.round) instead of truncating. Verified all test suites pass.
Merge Commit: Merge Clone A changes and resolve conflicts - quizana.louise
Push Result: Successfully pushed the merge commit to remote.
Task 3 Evidence
<img width="1918" height="1079" alt="Screenshot 2026-09-21 210857" src="https://github.com/user-attachments/assets/3db41c71-6a02-4c02-9eef-e698cebdbfe6" />



Task 4: Diverge Again and Reconcile with a Rebase
Branch: feature/overtime-pay
Objective: In Clone A (without fetching Clone B's push), make an additional change to calculatePay by extracting OVERTIME_RATE = 1.5.
Commit: Extract overtime rate constant - quizana.louise
First Action (Push): Attempted push was rejected (! [rejected] (non-fast-forward)).
Reconciliation: Executed git fetch origin followed by git rebase origin/feature/overtime-pay.
Resolution: Resolved rebase conflict in shifts.js preserving both the constant abstraction and Math.round. Continued rebase and successfully pushed without force.
Task 4 Evidence (Rejection & Rebase Resolution)
<img width="1918" height="1079" alt="Screenshot 2026-09-21 211102" src="https://github.com/user-attachments/assets/ffcaf01b-c88e-4da3-8dab-91950876fbe6" />



Task 5: Merge into Main
Branch: main
Objective: Check out main, merge the completed and tested feature/overtime-pay branch into main.
Merge Commit: Merge branch 'feature/overtime-pay' into main - quizana.louise
Push Result: Successfully pushed updated main branch to remote.
Task 5 Evidence
<img width="1918" height="1079" alt="Screenshot 2026-09-21 211515" src="https://github.com/user-attachments/assets/b611dccd-0dda-4b3f-8fff-62893d65bf3e" />



Task 6: Tag and Release
Tag: v1.0-synced
Action: Created annotated tag v1.0-synced on the final commit and pushed tags (git push origin --tags).
Task 6 Evidence
<img width="1918" height="1079" alt="Screenshot 2026-09-21 211947" src="https://github.com/user-attachments/assets/af279a0b-dd08-4c5b-b6dc-3a7afd25a073" />


Reflective Questions & Written Analysis
1. What did the rejected push error message tell you, and why did it happen?
The rejected push error message indicated that updates were rejected because the remote branch contained commits that were not present in the local repository, advising to fetch and integrate remote changes before pushing again. This occurred because another clone had already pushed new commits to the same branch, leaving the local branch's history out of date. Git blocked the push to protect against non-fast-forward updates that would overwrite remote work.

2. What's the actual difference between how you resolved Task 3 (merge) vs Task 4 (rebase)?
In Task 3, git merge preserved the historical timeline by combining both divergent branches into a brand new merge commit with two parents. In contrast, Task 4's git rebase rewrote history by unwinding the local commit and replaying it directly on top of the updated remote base. This rebase resulted in a clean, linear history without creating an extra merge commit, but it produced a new commit hash. Merging preserves the true historical record, while rebasing linearizes history by rewriting commits.

3. What one habit would have avoided both rejected pushes in this lab?
Consistently fetching or pulling remote changes (git fetch or git pull) immediately before starting new work and right before pushing would have prevented both rejections. Frequently synchronizing with the shared repository ensures that local work is always built directly on top of the latest remote commits. This prevents the local branch from silently falling behind and diverging from the remote branch.

4. Which approach — merge or rebase — would you default to on a shared team branch, and why?
I would default to git merge on a shared team branch because it does not rewrite public history. Since git rebase creates new commit hashes, rebasing a shared branch forces teammates to reconcile diverged local states, frequently causing duplicate commits and confusion. Merging safely preserves every collaborator's original commits and explicitly records when branch histories were integrated. Consequently, merge is significantly safer and more reliable for collaborative team branches.
