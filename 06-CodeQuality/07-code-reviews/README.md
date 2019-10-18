# Code Reviews
Agile teams are self-organizing, with skill sets that span across the team.
This is accomplished, in part, with code review.
Code review helps developers learn the code base, as well as help them learn new technologies and techniques that grow their skill sets.

## So, what exactly is a code review?
When a developer is finished working on an issue, another developer looks over the code and considers questions like:

* Are there any obvious logic errors in the code?
* Looking at the requirements, are all cases fully implemented?
* Are the new automated tests sufficient for the new code? Do existing automated tests need to be rewritten to account for changes in the code?
* Does the new code conform to existing style guidelines?

Code reviews should integrate with a team’s existing process. For example, if a team is using task branching workflows, initiate a code review after all the code has been written and automated tests have been run and passed–but before the code is merged upstream. This ensures the code reviewer’s time is spent checking for things machines miss, and prevents poor coding decisions from polluting the main line of development. 

## What's in it for an agile team?
* Code reviews share knowledge
* Code reviews make for better estimates
* Code reviews enable time off / decouple team members to code
* Code reviews mentor newer engineers

>**PROTIP:**
>Keep in mind, code review is not just a senior team member reviewing a junior team member’s code. Code review should happen across the team in every direction. Knowledge knows no bounds! Yes, code review can help newer engineers, but by no means should it be used solely as a mentoring exercise. 

## But code reviews take time!
Sure, they take time. But that time isn't wasted–far from it.
When done right, code reviews actually save time in the long run.
Here are three ways to optimize for that. 

### Share the load
Many teams require two reviews of any code before it's checked into the code base. 
Sound like a lot of overhead? 
Really, it's not. 
When an author selects reviewers, they cast a wide net across the team. 
Any two engineers can give input. 
This decentralizes the process so that no one is a bottleneck, and ensures good coverage for code review across the team.

### Review before merging
Requiring code review before merging upstream ensures that no code gets in unreviewed. 
Which means that the questionable architectural decisions made at 2am and the improper use of a factory pattern by the intern are caught before they have a chance to make a lasting (and regrettable) impact on your application.

### Use peer pressure to your advantage
When developers know their code will be reviewed by a teammate, they make an extra effort to ensure that all tests are passing and the code is as well-designed as they can make it so the review will go smoothly. That mindfulness also tends to make the coding process itself go smoother and, ultimately, faster.

>**_Don’t wait for a code review if feedback is needed earlier in the development cycle._** 
>Feedback early and often makes for better code, so don't be shy about involving others–whenever that may be. 
>It'll make your work better, but it also makes your teammates better code reviewers. And the virtuous cycle continues....!

### TODO
* Create a new git branch on your webapp
* Find an improvement that can be made and commit it
* Create a pull request for that branch to be merged into master and add someone in the team that is free to do a quick code review
* If your reviewer has any issues that can be resolved - fix them
* Once completed, you can approve the pull request

***Content from this document is adapted from https://www.atlassian.com/agile/software-development/code-reviews***

### [Finish Section >>>](../)