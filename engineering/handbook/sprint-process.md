# Sprint process

Engineering works in two week sprints. Sprints begin with a planning meeting, where we allocate already-grooomed, prioritized and 
estimated issues into the new sprint. Issue estimations are re-assessed if need be, issues deemed too complex are withheld and
broken down to be part of a later sprint, and issues are added until we feel there are enough small + big estimate task(s) per
person in a sprint.

We do a mid-way sprint standup, which serves to do course corrections, identify blocks and/or provide help.

At the end of the sprint there is a sprint retrospective, where we look back on the past two weeks in terms of what went well, and
what we could improve. The main purpose of this is to look at process and _why_ something went wrong or well, so that we can avoid
or encourage appropriately. Note: It's not a blame game!

Sprint grooming is held at regular intervals according to necessity, not necessarily tied to the sprint cycle per se. The 
purpose of grooming is to ensure that issues are: (i) clear, (ii) detailed as needed, (iii) broken down as much as makes sense,
(iv) estimated and (v) prioritized.

## Estimation

In order to make sure that we accept a reasonable amount of work into sprints, we estimate user stories. Estimation is done in terms of story points, using a [Fibonnaci scale](https://en.wikipedia.org/wiki/Fibonacci_scale_(agile)). The estimate is based on effort, which is a combination of complexity of the story, time usage and general size. For example a story that has many unknown factors that need resolving but may produce relatively little code changes may have a higher points estimate than a story that involves a simple change applied to many git repositories at once.

To help get the engineering team aligned on how they think about points estimates, a baseline story was estimated by the team. The story was an [MVP of using Jenkins shared libraries](https://makewisedk.atlassian.net/browse/SCAUT-79) which was estimated as being 5 points. When the team itself changes significantly, a new baseline will be picked and agreed upon. Significant team changes includes team members joining or leaving.

Bugs are not given points estimates. This is because bugs are not contributing to new value added, but instead are fixing problems in value that has already been added. If many bugs get added to sprints and this affects sprint velocity, that is an acceptable outcome for the team. This reflects the cost of bugs and any problems with our testing and verification process, and would be a good talking point between the team and product owner during sprint retrospectives.
