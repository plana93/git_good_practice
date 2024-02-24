The command ```--amend``` is used to modify the last commit. It is useful when you forgot to add,delete some files or change something or modify the commit message. 

```
#edit amd modify what you want correct 
git add . 
git commit --amend # it open the editor to give you the opportunity to modify the commit (if you want update it)
```

<span style="color: red">
If you run git commit --amend after already pushing the previous commit, it can cause issues, especially when collaborating with others on the same repository. Here's what might happen:

Already shared commit:

If you have already shared the previous commit by pushing it, your remote repository already has a copy of that commit. If you run git commit --amend and modify the commit, you will create a new commit with a new hash and a new history. The previous commit will remain unchanged in the remote repository.
Force push required:

If you try to push the new commit after git commit --amend, Git will likely warn you that the history has been changed and that a force push is needed to overwrite the history in the remote repository. However, force pushing can cause issues for other collaborators on the repository, especially if they have worked based on the original commit.
Collaboration risks:

Modifying the history of already shared commits can pose collaboration risks. Other collaborators who based their work on the original commit may face difficulties integrating the changes since the history would diverge.
In general, it is not recommended to alter the history of commits after pushing to a shared repository. If it's absolutely necessary to make changes to an already shared commit, it's best to discuss it with the team and decide collectively how to handle the situation. If possible, avoid force pushing in a collaborative context.
</span>
