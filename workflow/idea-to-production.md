### From Idea -> Production
Any feature addition to the platform transitions from a _design_ phase, to _implementation_ and finally _release_. How
this happens depends on the **type** of feature, particularly whether it is user-facing or not, and whether it contains
changes to, or exposes, sensitive data.

User-facing features are described, mocked up and discussed in
[Design Research](https://makewise.myjetbrains.com/youtrack/agiles/99-17/100-23), while non-user facing features are
discussed in the [SCAUT Platform project](https://makewise.myjetbrains.com/youtrack/projects/a943db9e-ae00-4e77-9f6b-ad6cf1d879fd).

Once a feature is ready to be implemented, it becomes a part of the sprint cycle where it is implemented on a short-lived feature
branch and eventually becomes a pull-request towards the `develop` branch (TODO: Link to git flow stuff). If the feature is deemed 
_sensitive_ then it becomes part of a prolonged QA process on either a PR-specific deployment or on the development environment;
otherwise it receives just superficial QA by peer reviewers as part of the Pull Request process and eventually as part of a release
candidate.

Release candidates happen at different rates depending on whether it is the mobile app, web frontend or backend. For the mobile app,
releases are less frequent and much more thoroughly QA'd, in order to avoid angering patients. For the web frontend and backend, 
releases are as frequent as we can reasonably push them out. Some release candidates will happen slower than others, if they
contain features deemed _sensitive_.

### From Bug -> Production
Bugs are reported in [YouTrack](https://makewise.myjetbrains.com/youtrack/issues) under the SCAUT Platform project, where they
are then inspected regularly by Engineering to determine whether they are critical or not. Critical bugs interrupt sprints and
will be looked at immediately, while non-critical bugs become a regular part of planning a sprint. 

Critical bugs may end up being hotfixed straight onto the production branch (and then backported to development), while 
non-critical bugs follow basically the same flow as 'ideas' above.
