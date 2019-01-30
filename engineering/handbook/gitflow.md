# Git workflow

### Naming branches
Each software repository should have the following branches:

* `master`: Production, each version deployed should be tagged. Changes merged into this branch should ideally only come from `develop` branch or hotfix branches.
* `develop`: Main development branch that should be fairly stable. Anything merged into this branch must be peer reviewed first.
* hotfix branches: For hotfixes that will go directly into `master`. They should be named after issue id with `hotfix` prefix, e.g. `hotfix-SCAUT-321`.
* feature branches: For work that will be merged into develop. They should be named after issue id, e.g. `SCAUT-123`.

### Overview

tl; dr -> we use the [git flow](https://nvie.com/posts/a-successful-git-branching-model/) approach to branching, with peer-review on all PRs. We adhere to rebasing not merging, and we squash to a single, or as few as is reasonable, commit(s).

All work except incredibly time-critical hotfixes is done via Pull Requests. This means that working on an issue begins by checking out
a branch from its parent (e.g., `develop`), working on it a bunch and then opening a pull request when you are ready for the code to
be reviewed. Once a PR is under review, you should stop rebasing/altering history unless absolutely necessary - as that will mess
with the comment/review history on GitHub. Fix problems identified during the review by _adding_ commits only.

Once the pull request is accepted, you should clean it up according to our rules about the format of git commits (see below). It can
then be merged into its parent branch. Below are some requirements on the structure and format of commits that get merged into
`master`/`develop`, that you should check if your squashed PR adheres to.

### Git commit rules

A git commit must make sense on its own, as a stand-alone unit of change. Additionally, there are some restrictions on how to write commits to ensure a consistent style and form:

* Commit text and messages are written in the current tense, e.g., "Remove logout button from application", not "Removed logout button"
* Commit titles must refer to the issue they relate to by prefixing the issue id e.g., `SCAUT-123 Remove logout button`
* Commit bodies must generally include a list of dash-prefixed items that briefly and specifically ensure you understand exactly what has changed. For example:
    * Bad commit body line: "Deprecate unneeded API route" (no dash, and too vague)
    * Good commit body line: "- Remove /api/v2/patient/foo"
    * Bad commit body line: "- Refactored patient search" (past tense, too vague)
    * Good commit body line: "- Modify searchPatients to always filter based on current users Clinic access"
    * Bad commit body line: "- Add getPatientProfilesInBulk because it is useful for the web API to be able to fetch them like this" (unnecessarily verbose; no need to specify **why**)
    * Good commit body line: "- Add getPatientProfilesInBulk to fetch multiple profiles at once"
* Commits can be used to execute commands in YouTrack, such as altering the state of the issue. You should use this
to your advantage: You can move an issue to `Done` state automatically, f.ex. See [VCS actions](https://www.jetbrains.com/help/youtrack/standalone/Apply-Commands-in-VCS-Commits.html) for more information on this.

**Suggestions for working with git and the git history**

These are by no means a requirement, but they may help you not get into bad situations. Avoid them at your own peril ;)

* Commit often locally, and continually pull in changes from the parent branch by git pull → git rebase -i, rebasing your local branch on top of the history of the parent branch. Do not merge the parent branch into your branch - ever.
* Avoid long-running branches like the plague, as they tend to become harder and harder to work on. Unless you have a **very good reason**, a branch generally shouldn't last longer than couple of days. Big changes or features should ideally be split into self contained units.
* Don't squash your PR into a single commit before the review has concluded; it's useful for the reviewer to see how the PR got to it's current state.
* Once a PR has been accepted, there is some cleanup work to do:
    * There should be no intermediary commits, no commits with typo’s or bad descriptions, and **all** commits should refer to an issue.
    * As a general rule, squash the entire branch into as few commits as possible, each of which relate to its own issue. **Almost all branches should just be a single commit**. The only commit(s) allowed that don't relate to an issue are trivial changes like removing dead code or reformatting, which importantly do not change code functionality at all.
    * Ensure that the PR title and body contains the same information that the commit does, and that each commit adheres to the "Git commit rules" above.

### Example
Suppose we have an issue with the id SCAUT-123. Applying the above could look like the following:

1. Create a new branch for the issue: `git checkout -b SCAUT-123`
2. Do a bunch of work on the feature.
3. Once the work is done, open a pull request for the issue: `git pull-request` or open one via the GitHub UI.
    1. PR title: `SCAUT-123 Remove logout button`
    2. PR body:
    
    ```
    - Remove logout button in profile menu
    - Fix profile menu margins
    ```
4. Assign reviewer(s) on Github. The issue will now undergo "Peer Review" as per above.
5. Once the PR has been accepted, we must now clean up the commits.
    1. Pull newest develop: `git checkout develop && git pull`
    2. Rebase our PR branch against develop: `git checkout SCAUT-123 && git rebase -i develop`
    3. In the interactive rebase, we `squash` all the commits into a single commit. This will let us interactively edit the commit message, which we clean up and ensure it follows the above rules on commit messages.
      - We make sure to put `^SCAUT-123 Done` in the commit text somewhere, as that will automatically move the issue to `Done` state in YouTrack
    4. Afterwards, check that the history looks clean and proper with `git log`
6. Merge the PR into develop: `git checkout develop && git merge SCAUT-123 && git push`
