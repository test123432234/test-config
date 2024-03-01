# test-config
config setup testing for clean-and-green-philly 

## the goal
![Screenshot 2024-02-29 184556](https://github.com/test123432234/test-config/assets/13136141/2b022161-1540-4981-add2-4d6673401885)

## the obstacle 
GitHub doesn't let you restrict who can perform a merge.

## facts & tools
- CODEOWNERS file can enforce code review
- branch restriction can control who commits a branch
- github has a merge que feature (useful for branches)

## current attempt
```mermaid 
flowchart TB
  subgraph PROD["the Brandon step"]
      direction TB
      coFile --> prPRODTeam["Org. Team: PROD"] -->  prodDone["merge to STAGING into Main"] 
  end
  
  subgraph STAGING["the Than step"]
      direction TB
      coFile --> prQATeam["Org. Team: StagingQA"]
      prQATeam -- "approves PR" --> devDone[" Dev merges to STAGING branch"] --> branchGating --> prQADone["QA team member creates PR For MAIN branch"]
      prQATeam -- "disapproves PR" --> devItr
  end
  
  subgraph TOOLS["the tools"]
      direction TB
      branchGating["github MAIN branch commits restricted to team PROD & StagingQA"]
      
  end

  subgraph DEV["the dev flow"]
      direction TB
      devItr["dev iteration"] -.-> pr["pull request to Staging"] -.-> coFile["PR assignemnts in CODEOWNERS files"]
  end

```
