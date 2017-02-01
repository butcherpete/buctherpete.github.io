---
title: Git Merges
tags: [git]
keywords: git 
last_updated: February 1, 2017
summary: Git merge notes 
sidebar: notes_sidebar
permalink: git_merge.html
folder: notes 
---

## Pulling from "Their" Branch

To pull all changing from another branch:

```
$ git checkout branchA
$ git merge -X theirs branchB
```

In this context, "ours" is branchA and "theirs" is branchB.

For example:

```
$ git checkout release
$ git merge -X theirs dev
```

## Cherry Picking Commits

In Git, a cherry-pick is like a rebase for a single commit. Its a way to introduce changes from one branch to another.

Cherry pickinge enables you to select a patch that was introduced in a specific commit and apply it onto a branch. Useful if you want to integrate a single commit from a branch and ignore others.

To pull a single commit:

```
$ git cherry-pick e43a6
```

To pull the most recent commit: 

```
$ git cherry-pick dev 
```

This applies the change introduced by the commit at the tip of the dev branch and create a new commit with this change.

To pull and accept commit:

```
$ git cherry-pick 5b0ee10 --strategy-option theirs
```
Why can't I cherry-pick by tag?

## Overwriting All Local Changes

To overwrite a local repo with a remote:

```
git fetch origin
git reset --hard origin/master
```
