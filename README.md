# Git Cheatsheet
_Conventient Git cheatsheet_

#### Switch branch
```
git checkout <branch> -> git checkout dev
```

#### Switch to new branch
```
git checkout -b <branch> -> git checkout -b feature-branch
```

#### Remove local branch
```
git branch -d <branch> -> git branch -d feature-branch
```
Use `-D` to force delete (including local changes).

#### Remove remote branch
```
git push origin --delete <branch> -> git push origin --delete feature-branch
```

#### Stage all local changes
```
git add .
```

#### Undo all local changes
```
git checkout .
```

#### Commit
Commit and add message in an editor:
```
git commit
```

Commit with commit message:
```
git commit -m "Commit message here"
```

#### Change last commit message:
```
git commit --amend
```
Use ` -m "New commit message"` to specify the new message directly.

#### Undo last commit but keep changes:
```
git reset HEAD~1
```

#### Rebase with remote:
```
git fetch <remote> -> git fetch upstream
git rebase <remote>/<branch> -> git rebase upstream/master
git push -f
```

#### Reset pushed commits
Undo pushed commits (eg. to undo a merge/rebase). Reset the commits back to the commit specified hash:
```
git reset --hard <sha>
```
Force-push the changes:
```
git push -f
```

#### Add a remote:
```
git remote add <name> <git> -> git remote add upstream https://github.com/organization/repo.git
```

#### Rebase with remote branch
```
git rebase <remote>/<branch> -> git rebase upstream/master
```
Force-push the changes:
```
git push -f
```

#### Squash commits
If you want to squash (merge) all the commits into one, follow this step too; otherwise, go to the next step.

First find the commit that is the base of your branch:

```
git merge-base fix-45 master
```
Copy the hash that is returned. Execute an interactive rebase using this command:
```
git rebase --interactive <hash>
```
Replace <hash> with the copied hash.

An editor will be opened which shows all the commits in your branch. It looks like:
```
pick 1fc6c95 do something
pick 6b2481b do something else
pick dd1475d changed some things
```
When using VIM, press I to go to insert mode. For every line, except the first, change pick to squash. (VIM: press Esc to exit insert mode, then :w to save the file and :q to quit VIM)

A new editor pops up with all the commit messages combined. Create the final commit message. Lines starting with # will be ignored. The same VIM commands as above apply here too.

Saving this file will squash all the commits into one, and you're done.

#### Tag a commit
```
git tag -a <name> <sha> -m <message> -> git tag -a v1.0 9fceb02 -m "Version 1.0"
```
Push the tag:
```
git push --tags origin <branch> -> git push --tags origin master
```

#### Duplicate (ambiguous) refs:
Remove the refs from `.git/refs/heads` -> `rm .git/refs/heads/<name>`
