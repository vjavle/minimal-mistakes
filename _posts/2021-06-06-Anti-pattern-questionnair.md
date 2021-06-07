---
layout: post
title: Anti pattern questionnair
published: true
---
# Anti pattern questionnair

To identify possible anti-patterns, these are the simple questions to be asked of a team.

| Question | Answer | AntiAgile | Anti-devops | Anti CI | Anti CD | Why |
| :------- | :----: | :-------: | :---------: | :-----: | :-----: |  :----: |
| Do you have more than 3 statuses (ToDo, InProgress, Done) for a backlog item? | Yes | ✓ |  | ✓ |   | [↓](#Are-there-more-than-3-statuses-(ToDo,-InProgress,-Done)-for-a-backlog-item?) |
| Is there a devops team? Or do you do devops? | Yes |   | ✓ |  |   | [↓](#Is-there-a-devops-team?-Or-do-you-do-devops?) |
| Is team cross skilled and cross functional? | Yes |   | ✓ | ✓ |   | [↓](#Is-there-a-devops-team?-Or-do-you-do-devops?) |


### Do you have more than 3 statuses (ToDo, InProgress, Done) for a backlog item? [![Anti-Agile](https://img.shields.io/badge/<Anti>-<Agile>-<Red>.svg)](https://shields.io/)
- [Agile manifesto](https://agilemanifesto.org) emphasizes a working product over complicated process.With a multi status complex workflow, a large process overhead is added rather than creation of working product
- Statuses are driven by a workflow. Too many statuses in a workflow means:
	- If time spent in each status is worth recording, than too many statuses combined together indicate a longer, hence anti-Agile iteration. _The fundamental Agility principle is FAIL FAST, LEARN AND APPLY CORRECTION FAST_. Longer iteration make failures correction longer (more work piled up due to longer iteration) & later (longer iteration to realize failure).
	- Too many stauses and complicated process can be hard for tem to remember and follow and can cause
[![Confusion](https://raw.githubusercontent.com/vjavle/vjavle.github.io/master/assets/images/sprintconfusion.png)](http://www.youtube.com/watch?v=Bw5LuY31C7w)

Most teams which start of multistage workflow approach with a goal of ultra optimizing time spent on each stage. This needs elaborate **time capture** and **reporting** mechanism for every workflow stage. This is a large process management overhead, which defeats the purpose of simplicity in Agility.
As is software is complex, some waste is inevitable. The point of smaller Agile iteration (e.g. Sprint) is to accept but reduce the waste.

### Is there a devops team? Or do you do devops? (yes)
- devops is a culture, not a team
- You don't DO devops. You adopt devops culture
- You do not have devops culture. The devops team is a renamed CI/CD or release team
- devops is cultural transformation of removing boundaries between development (including testing) and operations (infrastructure provisioning, post deployment support)

### Is team cross skilled and cross functional? (Or is there a separate database team? Or is there a separate testing team?) - (yes)
- At the least , Continuous Integration is less Continuous within the team, which essentially leads to being anti Agile. My definition of cross skilled is when each team member of the team can work on at least 2 layers of a functional stack (e.g. UI and Services or Services and DB or DB and Infrastructure code). Cross functional means, can a developer function as a tester or vice versa or can each team member perform a function of production support.
