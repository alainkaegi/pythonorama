# Extreme Programming Coding Steps
## Overview
You're involved in an Extreme Programming project, your team has met with the customer and done initial planning, and now you and your pair programming partner are ready to start coding. This document gives a checklist to go through as you work. (Don't worry, there's still *plenty* of room for creativity and problem-solving.)

Don't skip steps! That way lies disaster.

Don't spend hours in any one step. Keep moving so that commits and merges are frequent. There are few things less pleasant than merging two branches that haven't communicated with each other in weeks.

**The navigator should keep this page open and always know where you are in this checklist.**

1. [Choose a task](#1-choose-a-task)
    1. [Choose a story](#1i-choose-a-story)
    1. [Choose a task](#1ii-choose-a-task)
1. [Get the latest version of your team's work](#2-get-the-latest-version-of-your-teams-work)
    1. [Make sure you are in a clean state](#2i-make-sure-you-are-in-a-clean-state)
    1. [Pull everything](#2ii-pull-everything)
    1. [Check out your branch](#2iii-check-out-your-branch)
    1. [Merge from `main`](#2iv-merge-from-main)
1. [Write/edit code](#3-writeedit-code)
    1. [Make sure you are in a clean state and on the right branch](#3i-make-sure-you-are-in-a-clean-state-and-on-the-right-branch)
    1. [Unless you're just refactoring, write new unit tests](#3ii-unless-youre-just-refactoring-write-new-unit-tests)
    1. [Write/edit code](#3iii-writeedit-code)
    1. [Run tests; if they fail, go back to (3.iii)](#3iv-run-tests-if-they-fail-go-back-to-3iii)
    1. [Commit](#3v-commit)
    1. [Go back to (3.ii) unless you've finished a task or it's almost the end of the session](#3vi-go-back-to-3ii-unless-youve-finished-a-task-or-its-almost-the-end-of-the-session)
1. [Share your work with your team](#4-share-your-work-with-your-team)
    1. [Get the latest version of your team's work](#4i-get-the-latest-version-of-your-teams-work)
    1. [Issue a pull request](#4ii-issue-a-pull-request)
    1. [Review code](#4iii-review-code)
    1. [Move on to next task or merge](#4iv-move-on-to-next-task-or-merge)
    1. [If it's not the end of the session, go back to (1)](#4v-if-its-not-the-end-of-the-session-go-back-to-1)

## 1 Choose a task
### 1.i Choose a story
On the project board, you and your partner should be assigned to *one* card in the `In Progress` column. If not (e.g., because you just finished a story), pick a new one from the `This Iteration` column; if there aren't any, pick a story from the top of the `Backlog` column. Don't skip ahead to a story that looks easy or interesting; respect the customer's priorities about what to work on next.

### 1.ii Choose a task
If the story has a checklist of tasks in it, pick one of the tasks in the list.

## 2 Get the latest version of your team's work
### 2.i Make sure you are in a clean state
Remember that you must always be in a clean state before trying to do anything else with Git or GitHub; failure to do so is a good way to lose your work. If you are *not* in a clean state, you need to either *commit* or (on rare occasions) *throw away your work since the last commit* before proceeding.

#### To check if you are in a clean state
```
git status
```
The resulting message tells you what branch you're on if you have changes since the last commit. It should end in
```
nothing to commit, working tree clean
```

> [!IMPORTANT]
> The status message also tells you what branch you're on. If somehow you're on `main` or in a headless state, [create a branch](#2.iii-check-out-your-branch) before committing.

#### To commit
The instructions below also push your changes up to GitHub *on your branch*. There's nothing wrong with doing this every time you commit locally. You should *definitely* push when you make the last commit in a session.

To add a new file to version control:
```
git add yourfile
```

To commit:
```
git commit -am 'Your commit message here'
```

You should also push your code up to GitHub:

```
git push
```

#### To throw away your work since your last commit
> [!CAUTION]
> This is usually *not* what you want. Only do this if you are absolutely sure you want to throw away all changes since your last commit.

```
git reset --hard HEAD
```

### 2.ii Pull everything
Pulling both fetches the remote versions of all branches and tries to merge them into your local branches. This *shouldn't* result in any merge conflicts. If it does (because you and someone else were committing on the same branch), you'll have to resolve the conflicts.

```
git pull --all
```

### 2.iii Check out your branch
> [!IMPORTANT]
> You should never do any coding while on the `main` branch. Also, two different programming pairs should never be working on the same branch.

If you're creating a new branch:
```
git checkout -b branchname
```
If you're just checking out an existing branch, leave out the `-b`.

### 2.iv Merge from `main`
This step merges all of the changes from the `main` branch (including work by other members of your team) into your branch.

```
git merge main
```

Make sure that the merge worked. If you get an error message indicating a merge conflict, resolve the conflict by editing the offending files and then committing again. **_Do not do anything else until you have resolved the conflict._**

## 3 Write/edit code
### 3.i Make sure you are in a clean state and on the right branch
This is the same as (2.i), but also make sure that you are on the correct branch.

### 3.ii Unless you're just refactoring, write new unit tests
In test-driven development, every change should be either refactoring or trying to pass some test. The new tests should fail at this point. Be sure to commit them as described in (2.i).

### 3.iii Write/edit code
You've trained for this!

### 3.iv Run tests; if they fail, go back to (3.iii)
If they pass, bask in the glow of the green bar.

### 3.v Commit
See (2.i) for instructions on committing.

### 3.vi Go back to (3.ii) unless you've finished a task or it's almost the end of the session
You will probably spend most of your time in (3.ii) through (3.vi). This should result in very frequent commits, ideally every few minutes.

## 4 Share your work with your team
You've finished a task, so it's time to incorporate it into the `main` branch.

### 4.i Get the latest version of your team's work
This is exactly the same as step (2).

### 4.ii Issue a pull request
Go to the GitHub website for your project. Choose the branch you're on (using the selector on the left end of the line that has the green `Clone or download` button on the right) and choose `New pull request`.

This tells your team, "Our branch has some new functionality. Let's merge it into `main`." Confusingly, it does not mean "I want to pull" but rather "I want the team to pull from my branch into the `main` branch."

Move your story to the `Completed in Branch` column.

### 4.iii Review code
Find another pair in your team to review your code. You may have to wait a few minutes for them to make their next commit so that they can give you their full attention.

Working with this other pair on GitHub, review the changes you made. Some things to consider:

- Does the new code compile, run, and perform as advertised?
- Are there thorough unit tests?
- Do the tests pass?
- Is the code clean and well-documented?
- Is there any way the code should be improved? (This is not asking the software to have additional features; do one thing at a time.)

If not everyone is satisfied, close the pull request rather than approving it. You will create a new one after you resolve the issue. Go back to (3.ii).

If everyone is happy, move the story to `Reviewed`.

### 4.iv Move on to next task or merge
If the story has more unfinished tasks, move it back to `In Progress` and go back to (1.ii).

If this was the last task, click on `Merge Pull Request` on GitHub and conform. Resolve any issue with the merge; there usually won't be any. Move the card to `Merged`.

### 4.v If it's not the end of the session, go back to (1)
You have finished something and are now ready to move on to the next thing!
