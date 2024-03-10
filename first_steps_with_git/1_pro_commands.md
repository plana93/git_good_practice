## `--amend`

The command `--amend` is used to modify the last commit. It is useful when you forgot to add,delete some files or change something or modify the commit message. 

```
#edit amd modify what you want correct 
git add . 
git commit --amend # it open the editor to give you the opportunity to modify the commit (if you want update it)

or 

git commit --amend --no-edit #if you have alredy pushed the previous commit, you need to force push
```
<details>
<summary><strong> Be carefull </strong></summary>
<font style="color: red">
If you run git commit --amend after already pushing the previous commit, it can cause issues, especially when collaborating with others on the same repository. Here's what might happen:

Already shared commit:

1) If you have already shared the previous commit by pushing it, your remote repository already has a copy of that commit. If you run git commit --amend and modify the commit, you will create a new commit with a new hash and a new history. The previous commit will remain unchanged in the remote repository.
Force push required:

2) If you try to push the new commit after git commit --amend, Git will likely warn you that the history has been changed and that a force push is needed to overwrite the history in the remote repository. However, force pushing can cause issues for other collaborators on the repository, especially if they have worked based on the original commit.
Collaboration risks:

3) Modifying the history of already shared commits can pose collaboration risks. Other collaborators who based their work on the original commit may face difficulties integrating the changes since the history would diverge.
In general, it is not recommended to alter the history of commits after pushing to a shared repository. If it's absolutely necessary to make changes to an already shared commit, it's best to discuss it with the team and decide collectively how to handle the situation. If possible, avoid force pushing in a collaborative context.

</font>
</summary>
</details>



## `reset --soft`

The commmand `reset --soft`will undo the last commit, keeping the files in your Working Directory and Index as they were in the previous commit. You can then make additional changes, if necessary, and proceed with a new commit.

```
git reset --soft HEAD^
# do something else to come up with the right tree ...
git add .
git commit -c ORIG_HEAD
```

<details>
<summary><strong> Be carefull </strong></summary>

**Uncommitted Changes:**

- Make sure you have committed all the changes you want to keep before executing the reset. Uncommitted changes in your Index will be lost.

**Shared History:**

- If you have already shared the commit you are undoing with other collaborators through a push, <ins>you could cause confusion in the repository's history.</ins> Avoid using git reset --soft after sharing commits.

**Use with Caution:**

- A soft reset is a powerful operation that modifies the repository's history. Ensure you fully understand the impact before using it, especially in collaborative contexts.


### Pratical example on what happen on the graph  

Initial Scenario (Local and Remote):
```
A -- B -- C (main, HEAD)
          \
           D (origin/main)
```


Where:

A, B, C are local commits.
D is the corresponding commit on the remote branch (origin/main).

After ```git reset --soft HEAD~1``` (Local):

```
A -- B (main, HEAD)
       \
        C
          \
           D (origin/main)
```
After the reset, main and HEAD move to commit B. The changes made in C are still present in your Working Directory and Index. **There is no impact on the remote repository so far.**

After a new local commit (Local):

```
A -- B -- E (main, HEAD)
       \
        C
          \
           D (origin/main)
```
After making new changes and committing E, your local graph is updated.

After git push (Remote):

```
A -- B -- E (main, HEAD)
       \
        C
          \
           D -- E (origin/main)
```

When you push, E is added to the remote repository. However, commit C remains in the local repository but is not present in the remote repository. 
**It's important to note that if others have already fetched or pulled changes from the remote repository before your push, they might have commit C in their local repository.** Therefore, coordinating with the team before using git reset --soft on already shared commits is advisable.

</summary>
</details>


## `rebase`

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



## Simple solution to squash last N commits together
```
git reset --soft HEAD~2  # N=2
git commit -m "new commit message"
git push -f
```