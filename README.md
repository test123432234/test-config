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
      prPRODTeam["Org. Team: PROD"] -->  prodDone["merge to STAGING into Main"] 
  end
  
  subgraph STAGING["the Than step"]
      direction TB
prQATeam{"Org. Team: StagingQA"}
      prQATeam -- "approves PR" --> devDone["Dev merges to STAGING branch"]
      devDone --> branchGating --> prQADone["StagingQA team member creates PR For MAIN branch"]
      prQADone --> coFile --> prPRODTeam

      prQATeam -. "disapproves PR" .-> devItr
  end
  
      branchGating["github MAIN branch commits restricted to teams: PROD & StagingQA"]
      coFile["PR assignemnts in CODEOWNERS files"]

  subgraph DEV["the dev flow"]
      direction TB
      devItr["dev iteration"] -.-> pr["pull request to Staging"] -.-> prQATeam
  end


```
