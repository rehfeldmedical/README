# Git workflow

### Naming branches
Each software repository should have the following branches:

* `master`: Production, each version deployed should be tagged. Changes merged into this branch should ideally only come from `develop` branch or hotfix branches.
* `develop`: Main development branch that should be fairly stable. Anything merged into this branch must be peer reviewed first.
* hotfix branches: For hotfixes that will go directly into `master`. They should be named after issue id with `hotfix` prefix, e.g. `hotfix-SCAUT-321`.
* feature branches: For work that will be merged into develop. They should be named after issue id, e.g. `SCAUT-123`. If you want to suffix with additional words, then _keep it short_ -- no `SCAUT-123-this-is-why-this-branch-exists-for-us`.

### Overview

We work using feature branches that get applied straight to `master` (or `develop` in the case of the mobile app), with 
peer-review on all PRs. Once reviewing begins, we _merge_ the parent branch into the PR until review(s) are done, so as 
not to destroy comment history. Once reviewing is done, we rebase & squash to a single / as few reasonable commit(s) as
possible, so merges into the parent branch are always fast-forward.

All work except incredibly time-critical hotfixes is done via Pull Requests. This means that working on an issue begins by
checking out a branch from its parent (e.g., `master`), working on it a bunch and then opening a pull request when you are
ready for the code to be reviewed.

Once the pull request is accepted, you should clean it up according to our rules about the format of git commits (see 
below). It can then be merged into its parent branch. Below are some requirements on the structure and format of commits
that get merged into `master`/`develop`, that you should check if your squashed PR adheres to.

### Git commit rules

You can learn a lot by just looking at our existing commits, and observing the general format and approach taken. Beyond
that, please read [RomuloOliveira's commit guide](https://github.com/RomuloOliveira/commit-messages-guide), which nicely
sums up a lot of our opinions on the subject as well. Finally, commits should refer explicitly to the issue ID to which they
are related, preferably as a prefix in the title, or in the commit body if it touches on multiple issues.

**Suggestions for working with git and the git history**

These are by no means a requirement, but they may help you not get into bad situations. Avoid them at your own peril ;)

* Commit often locally, and continually pull in changes from the parent branch by git pull → git rebase -i, rebasing your local branch on top of the history of the parent branch. Do not merge the parent branch into your branch - ever.
* Avoid long-running branches like the plague, as they tend to become harder and harder to work on. Unless you have a **very good reason**, a branch generally shouldn't last longer than couple of days. Big changes or features should ideally be split into self contained units.
* Once a PR has been accepted, there is some cleanup work to do:
    * There should be no intermediary commits, no commits with typo’s or bad descriptions, and **all** commits should refer to an issue.
    * As a general rule, squash the entire branch into as few commits as possible, each of which relate to its own issue or is very trivial in nature. **Almost all branches should just be a single commit**. The only commit(s) allowed that don't relate to an issue are trivial changes like removing dead code or reformatting, which importantly do not change code functionality at all.
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
5. Reviewing takes a while, so underway you `git merge` the `develop` branch into it to keep it current.
6. Once the PR has been accepted, we must now clean up the commits.
    1. Pull newest develop: `git checkout develop && git pull`
    2. Rebase our PR branch against develop: `git checkout SCAUT-123 && git rebase -i develop`
    3. In the interactive rebase, we `squash` all the commits into a single commit. This will let us interactively edit the commit message, which we clean up and ensure it follows the above rules on commit messages.
      - We make sure to put `^SCAUT-123 Done` in the commit text somewhere, as that will automatically move the issue to `Done` state in YouTrack
    4. Afterwards, check that the history looks clean and proper with `git log`
6. Merge the PR into develop: `git checkout develop && git merge --ff-only SCAUT-123 && git push`
