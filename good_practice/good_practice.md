Create two branches from the main called feat/features_branch_1 and feat/features_branch_2.

Come back to the main branch, COMMIT, and PUSH some changes to a file, e.g., `good_practice.md`.

Modify a file (e.g., `good_practice.md`) in the feat/features_branch_1 branch, COMMIT, and PUSH this change.

Modify a file (e.g., `good_practice.md`) in the feat/features_branch_2 branch, COMMIT, and PUSH this change.

Update the other two branches with small updates.

Now we can see the procedure for the `rebase`.

```
git checkout feat/features_branch_1

git rebase main # it tries to perform the rebase automatically, but if it encounters conflicts, you need to manually resolve them. 
```

An alternative is 

```
git rebase --abort # to remove the negative effects of the previous rebase.
git rebase -i main   # -i is for the interactive operation 
```
Now you can decide which commits to make visible and which ones to squeeze (collapse with the previous one), delete (pay attention to this operation; please be sure that this specific commit is already on the main). Then, you can decide the final commit message.

If you interrupt a rebase to fix some commits, you can continue with the command git rebase --continue
```
# As in this case 
git add -u 
git rebase --continue 

git push --force
```
Then you can continue with a PR or with the merge operation

