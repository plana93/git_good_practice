create a new repository 
```
git init
```

to clone a repository 
```
git clone <repository>
```

to prepare the specific content staged for the next commit 
```
git add <file>
git add .  # add all files
git add -u . # add only modified file, no the new ones
git add -A # add all files
```

Show the working tree status, more in details the differencies between:
- index file and the current HEAD commit
- working tree and the index file
- working tree and not tracked file by Git
```
git status
```
Show the working tree status, more in details the differencies between:
- index file and the current HEAD commit
- working tree and the index file
- working tree and not tracked file by Git
```
git status
```

Record changes to the repository
```
git commit -m "message del commit" # use a specific commit git commit -c HEAD # it use the last commit message
```
Show commit logs
```git log```
Show the actual branch and list all the available branches 
```git branch```

Change the current branch
```git checkout <branch>```

Update the current branch with the latest changes from the remote repository:

```git pull```

Upload local changes to the remote repository:
```git push```


# Example 

I created the 0_base_commands.md file 
```
git add .
or 
git add 0_base_commands.md

git commit -m <message>
git push 
```