# Setting Up a GitHub Repository
These are my notes on setting up a GitHub repository for a new project using PyCharm. I generally do this myself for research or Software Development projects.

## Create Project in IDE
I describe this [elsewhere](../development_tools/pycharm.md).

Optionally, set up a test directory and a sample class and test.

## Set Up .gitignore
1. `File` | `New` | `File`, `.gitignore`, add to version control when asked.
1. Give it the contents of the appropriate file [found here](https://gist.github.com/MOOOWOOO/3cf91616c9f3bbc3d1339adfc707b08a). Be sure to uncomment `.idea/` and `.vscode/` to avoid committing local IDE configuration information to the repository.

## Put Project Under Local Version Control
`VCS` | `Enable Version Control Integration`. Select Git and click `OK`.

## Create Repository on GitHub
1. Log into github.com.
1. Click on the green `New repository` button on the right.
1. Give the new repository the same name as the IntelliJ IDEA project.
1. Select `Private`; do not initialize with a README.
1. Click `Create repository`.
1. Copy the https URL to the clipboard.
   
## Push Initial Commit
1. `ctrl-k` to open version control tool window. (On a Mac, replace `ctrl` with `command`.)
1. Click on the project at the top so all files are selected.
1. Click `Commit and Push`.
1. Click on `Define remote`.
1. Paste the URL copied from the green `Code` button on GitHub.
1. Click `Push`.

## Protect the `main` Branch
On GitHub, in `Settings` | `Branches`, add a rule to the `main` branch that requires a pull request before merging. This prevents anyone from accidentally pushing to `main`.

## Add Other Team Members as Collaborators
On the GitHub website, from the repository: `Settings` | `Collaborators`.

## References
- [Set up a Git repository](https://www.jetbrains.com/help/idea/set-up-a-git-repository.html)
- [Practicing with IntelliJ and Git](https://gist.github.com/bgun/c7447ab0906517221b6b)
