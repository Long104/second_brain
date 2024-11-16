---
date: 2024-10-30T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# delete-commit-history

## Deleting the .git folder may cause problems in your git repository


```git

Checkout/create orphan branch (this branch won't show in git branch command):
git checkout --orphan latest_branch

Add all the files to the newly created branch:
git add -A

Commit the changes:
git commit -am "commit message"

Delete main (default) branch (this step is permanent):
git branch -D main

Rename the current branch to main:
git branch -m main
Finally, all changes are completed on your local repository, and force update your remote repository:

git push -f origin main
PS: This will not keep your old commit history around. Now you should only see your new commit in the history of your git repository.

```
