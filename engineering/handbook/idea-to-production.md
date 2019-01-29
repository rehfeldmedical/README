### From Idea -> Production
Any feature addition to the platform transitions from a _design_ phase, to _implementation_ and finally _release_. How
this happens depends on the **type** of feature, particularly whether it is user-facing or not, and whether it contains
changes to, or exposes, sensitive data.

![Design Research -> Engineering process](./dr-eng.png)

The design phase is governed primarily by [Design Research](../../design-research), where concepts transition from
[research](https://makewise.myjetbrains.com/youtrack/agiles/99-17/100-23) to 
[design briefs](https://makewise.myjetbrains.com/youtrack/agiles/99-21/100-31).

From a design brief, concepts are specified in more detail and turned into engineering tasks which enter the regular sprint 
cycle via sprint grooming. For more details on the sprint process itself, see ...

Once a feature is ready to be implemented, it becomes a part of the sprint cycle where it is implemented on a short-lived feature
branch and eventually becomes a pull-request towards the `develop` branch. See [git flow](/handbook/gitflow.md) for a more 
detailed explanation. If the feature is deemed _sensitive_ then it becomes part of a prolonged QA process on either a 
PR-specific deployment or on the development environment; otherwise QA occurs primarily by peer reviewers and designers as 
part of the Pull Request process and eventually as part of a release candidate.

Release candidates happen at different rates depending on whether it is the mobile app, web frontend or backend. For the mobile app,
releases are less frequent and much more thoroughly QA'd as the release process itself is heavy. For the web frontend and backend, 
releases are as frequent as we can reasonably push them out.

### From Bug -> Production
Bugs are reported in [YouTrack](https://makewise.myjetbrains.com/youtrack/issues) under the SCAUT Platform project, where they
are then inspected regularly by Engineering. Critical bugs interrupt sprints and will be looked at immediately, while 
non-critical bugs become part of the unplanned overhead of working on sprints.

Critical bugs warrant hotfixes directly on production, after which they are backported to development; non-critical bugs follow
roughly the same process that feature development does.
