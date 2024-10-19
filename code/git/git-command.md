---
date: 2024-10-20T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# Contents

<!-- toc -->

- [git-command](#git-command)
  - [git reset:](#git-reset)
  - [git revert:](#git-revert)
  - [git rebase:](#git-rebase)
  - [git merge:](#git-merge)

<!-- tocstop -->

# git-command

![[Pasted image 20241020010856.png]]

## git reset

- Moves the HEAD pointer and can modify the staging area and working directory.
  If you use git reset --hard, it discards changes in both the staging area and the working directory, moving the HEAD to 
  an earlier commit without keeping history of the undone commits.

## git revert

- Safely undoes a commit by creating a new commit that reverses the changes of a specific commit.
  History remains intact, making this a safer alternative to reset when working in a shared repository because no commits are lost.

## git rebase

- Reapplies commits from one branch onto another, essentially moving the base of a branch to a new commit.
  It creates a linear history, which can be cleaner, but be cautious when using it on shared branches since it rewrites commit history.

## git merge

- Combines two branches into one. All commits from the merged branch are preserved, keeping the full history.
  A new merge commit is created to record the result of the merge if there are any conflicts, keeping a non-linear history intact

## git merge --squash 
- is a Git operation that allows you to take all the changes from one branch and squash them into a single commit 
  on top of the branch you're currently on. This is different from a regular merge, where all commits from the feature branch are preserved.
  By squashing them into one, you're essentially saying, "Take all these changes as if they happened in a single moment." 
