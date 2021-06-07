---
layout: post
title: Anti pattern questionnair
published: true
---
# Anti pattern questionnair

To identify possible anti-patterns, these are the simple questions to be asked of a team.

<details>
  <summary><b>Do you have more than 3 statuses (ToDo, InProgress, Done) for a backlog item? </b> <img src="https://img.shields.io/badge/Anti-Agile-red.svg"></summary>
  <ul>
  <li> <a href="https://agilemanifesto.org">Agile manifesto</a> emphasizes a working product over complicated process.With a multi status complex workflow, a large process overhead is added rather than creation of working product  </li>
  <li> Statuses are driven by a workflow. Too many statuses in a workflow means:  
    <ol>
     <li> If time spent in each status is worth recording, then too many statuses combined together indicate a longer, hence anti-Agile iteration
       <ul>
       <li>The fundamental Agility principle is FAIL FAST, LEARN AND APPLY CORRECTION FAST</li>
       <li>Longer iteration make failures correction longer (more work piled up due to longer iteration) & later (longer iteration to realize failure)</li>
       </ul>
      </li>
     <li> Too many stauses and complicated process can be hard for tem to remember and follow and can cause [![Confusion](https://raw.githubusercontent.com/vjavle/vjavle.github.io/master/assets/images/sprintconfusion.png)](http://www.youtube.com/watch?v=Bw5LuY31C7w)  </li>
    </ol>      
  </li>  
  <li>  Many teams start with multistage workflow approach with a goal of ultra optimizing time spent on each stage. This needs elaborate <b>time capture</b> and <b>reporting</b> mechanism for every workflow stage. This is a large process management overhead, which defeats the purpose of simplicity in Agility.As is software is complex, some waste is inevitable. The point of smaller Agile iteration (e.g. Sprint) is to accept but reduce the waste   </li>
  </ul>
</details>

<details>
  <summary><b>Is there a devops team? Or do you do devops?</b> <img src="https://img.shields.io/badge/Anti-Agile-red.svg"> <img src="https://img.shields.io/badge/Anti-devops-red.svg"></summary>
  
  - devops is a culture, not a team
  - You don't DO devops. You adopt devops culture
  - If you have a devops team, You do not have devops culture. The devops team is a renamed CI/CD or release team
  - devops is cultural transformation of removing boundaries between development (including testing) and operations (infrastructure provisioning, post deployment support)
</details>

<details>
  <summary><b>Is team cross skilled and cross functional?</b> <img src="https://img.shields.io/badge/Anti-Agile-red.svg"> <img src="https://img.shields.io/badge/Anti-devops-red.svg"></summary>
  
  - Cross skilled - when each team member of the team can work on at least 2 layers of a functional stack (e.g. UI and Services or Services and DB or DB and Infrastructure code)
   - Cross functional - when a developer can function as a tester or vice versa or each team member perform a function of production support.
  - Is there a separate database team? Or is there a separate testing team? If you do, the spirit of continuous integration is lost right there.
  - Loss of continuous integration leads to anti agile (time lost waiting for other layer team to complete their work, only then to be integrated)
</details>
