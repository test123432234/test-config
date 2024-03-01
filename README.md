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
      branchGating{{"github MAIN branch
            commits restricted to
            teams: PROD & StagingQA"}}
      coFile{{"PR assignemnts in CODEOWNERS files"}}
      devItr["dev iteration & PR into STAGING branch"] -.->  coFile -.-> prQATeam
      devDone["Dev merges to STAGING branch"]
  
  subgraph PROD["the Brandon step"]
      direction TB
      prPRODTeam["Org. Team: PROD"] ==>  prodDone["merge to STAGING PR into MAIN branch"] 
  end
  
  subgraph STAGING["the Than step"]
      direction TB
      prQATeam{"Org. Team: StagingQA"} -. "pass PR" .-> devDone
      prQATeam -. "reject PR" .-> devItr
      devDone -.-> prQATask[["StagingQA team member creates a tagged merge commit"]] --> branchGating
      branchGating --> prQADone ==> coFile ==> prPRODTeam
      prQADone["StagingQA team member creates PR
            consisting of tagged commits
            For MAIN branch"] 
  end

```
