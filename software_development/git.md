# Git
## Overview
Git is a *version control system*, allowing you to keep track of multiple versions of a piece of software and coordinate changes with other developers. While manually making backup copies and emailing them around is fine for small programs, a tool like Git becomes essential for larger projects.

## Setup
### Installation
You can check if Git is installed on your system with this command:
```
git --version
```
If it isn't, it will complain. You can download it from the [Git website](https://git-scm.com/).

### Configuration
It's a good idea to run the commands below (with "your name" replaced appropriately) before using Git for the first time:
<pre>
git config --global user.name "<em>Your Name</em>"
git config --global user.email <em>yourname@yourdomain.edu</em>
git config --global init.defaultBranch main
git config --global core.editor nano
</pre>

(The last one determined what text editor Git will use. `nano` is built in on Macs, but you'll have to install it on a Windows machine. If you don't specify an editor, you'll get `vim`, which is [notoriously user-surly](https://qz.com/990214/a-million-people-have-visited-this-web-page-explaining-how-to-close-vim-a-notoriously-difficult-text-editing-program/).)

### Creating a Repository
A *repository* (or *repo*) is a set of snapshots of your files. Each one captures the state of your files at a particular point in time.

First create a directory and put a simple file in it, say, `file.txt`.

Now, within that directory, initialize the repository with this command:
```
git init
```
To see the status of the repository, use this command:
```
git status
```
The output tells you that you are on the `main` branch (more about branches later), you haven't made any *commits* (snapshots), and your file is still untracked. You have to explicitly tell Git which files to keep track of.

To add a file to version control:
```
git add file.txt
```
To make your first commit:
```
git commit -am 'Initial project version'
```
The part at the end is the commit message, explaining what you changed[.](https://xkcd.com/1296/)

If you check the status again, you will see that there is now "nothing to commit"; your current workspace of files matches the most recent commit. In general, working with Git is a cycle of making changes to your files and then committing them.

## Working With Git
### Committing
Edit a file. Alternately, create a new file and add it to version control.

Before committing, it's a good habit to always run `git status` to make sure things are in the state you think they're in.

Now commit:
```
git commit -am 'My poem is now twice as long'
```
Check the status again to make sure it worked.

> [!WARNING]
> You should *always* be in a clean state before trying to do anything else with Git. Usually this means committing.

> [!CAUTION]
> Occasionally you will decide that you instead want to throw away all of your work since the last commit. **If you are *absolutely sure* that you want to do this**, here is the command:
> ```
> git reset --hard HEAD
> ```

### Working With Past Commits
You can view the history of your repository with this command:
```
git log --oneline --graph --all
```
Each line represents one commit. It shows the hash (a number that identifies the state of the files) and the commit message. Some additional information like `HEAD -> main` tells you which one is the current commit.

For a example to work with, suppose the output of the log command looks like this:
```
* b361556 (HEAD -> main) My poem is now twice as long
* 456b316 Initial project version
```
If you want to go back to the previous version, do something like this:
```
git checkout 456b316
```
The hexadecimal number at the end is a prefix of the hash, enough to uniquely identify it. If you now examine your files, you'll see that they're back to the way they were after the first commit!

The newer commit (b361556) is still in the repository. Once something is in the repository, it's fairly difficult to destroy it.
> [!Caution]
> There are Git commands that allow you to modify the past, but it's a bad idea; you're likely to lose work, become your own grandparent, or tear a hole in the spacetime continuum.

To go back to the newer commit, you could use a similar `checkout` command. A much better idea is to use
```
git checkout main
```
to reattach `HEAD` to the front of the `main` branch.

> [!CAUTION]
> Never make commits in a detached HEAD state; it could cause you to lose work.

### Branches
It's best not to put commits on the `main` branch until you're sure you want to keep them. This is the time to create another branch. (You should be in a clean state before doing this, but it's okay if you're in a detached HEAD state.) Here's the command:
```
git checkout -b experiment
```
In this example, `experiment` is the name of your new branch. Now that you're on this branch, you can work as normal, modifying files and making commits. If you ever want to switch between branches, just do something like
```
git checkout branchname
```
where `branchname` is the name of the branch you want to switch to (e.g., `main`).

Now suppose your experiment went well and you want to merge the two branches. If you're currently on the `experiment` branch, you can merge any changes from `main` with:
```
git merge main
```
If you commit and merge often, and are a little lucky, merging will succeed automatically. Git is quite clever about this; if the changes on two branches are to different files, or even to different methods within the same file, Git can figure out how to keep both sets of changes.

Occasionally, though, it won't be obvious to Git how to combine the changes. This is the dreaded *merge conflict*. When this happens, Git will open your editor (you specified `nano` above) and ask you to resolve the conflict, i.e., edit the files to keep the parts you want.

> [!IMPORTANT]
> After you have the files the way you want them, commit again to complete the merge: `git commit`.

### Remote Repositories
Everything above has been about a local repository on your own machine. This is useful, but the real power of Git lies in collaborating with others, using a remote repository stored at someplace like [GitHub](https://github.com/).

Once you have cloned a remote repository to get a local one, you can work along in your local repository. You should avoid working on the `main` branch.

Occasionally, you'll want to incorporate the latest changes from the remote `main` branch into the branch you're working on (e.g., `experiment`). First make sure you are in a clean state, then:
```
git checkout main
git pull
git checkout experiment
git merge main
```
The `pull` command brought all the changes from the remote `main` branch into your local `main` branch. You then merged these into your `experiment` branch.

You can now push your branch to the remote branch:
```
git push origin experiment
```
This serves two purposes:
- It stores a remote copy, so you won't lose your work even if your computer is destroyed.
- Once you're confident that your code is working properly, it enables you to make a *pull request*, asking that your branch be merged into the remote `main` branch.

## Resources
- [Pro Git](https://git-scm.com/book/en/v2)
- Evans, [*How Git Works*](https://wizardzines.com/zines/git/)
- DZone, [Getting Started with Git Refcard](https://dzone.com/refcardz/getting-started-git?chapter=1)
- [A Visual Git Reference](http://marklodato.github.io/visual-git-guide/index-en.html)
- [Git](https://git-scm.com/)
- [GitHub](https://github.com/)
- [GitLab](https://about.gitlab.com/)
- [PyCharm Documentation on Git](https://www.jetbrains.com/help/pycharm/using-git-integration.html) (See the table of contents on the left side of this page.)
- [Untrack files already added to Git repository based on .gitignore](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)
- [Cache your GitHub credentials so you don't have to type your password every time you push](https://docs.github.com/en/github/getting-started-with-github/caching-your-github-credentials-in-git)
- [Version Control (Git)](https://missing.csail.mit.edu/2020/version-control/) (A video lecture with notes. Part of [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/) from MIT.)
- [How to Write Better Git Commit Messages – A Step-By-Step Guide](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)

## Questions
1. :star::star: How often should you commit?
1. :star::star: Where is a local repository stored?
1. :star::star: Does saving all of these copies of files use up a lot of disk space?
1. :star::star: Why would you ever have files in a directory that are not under version control?

## Answers
1. Often; several times an hour. Part of the point of Git is to allow you to go back to a previous commit if you make a mistake, so you want to have many options as to how far to go back.
1. In a hidden directory called `.git` inside the directory where you ran `git init`.
1. No. Git is clever enough to store only the differences between commits.
1. There is no reason to store compiled code, as it can be generated from the source code. Huge, unchanging data files that are available elsewhere are also often left out of version control.
