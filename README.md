# Port Support Engineer Assignment
**Full Name:** Asomugha Divine  
**Position Applied:** Support Engineer  
**Date Created:** 2025/11/08  
**Date Updated:** 2025/13/08  

---

## Overview

This repository contains my solutions for the Port Support Engineer assessment.  
It covers **Exercises #1–#4** as described in the assignment document, using **real data** from live integrations (no mock data).  

Evidence is provided through screenshots, logs, and test outputs.  
All sensitive credentials have been removed.  
The google doc submission for the task can be accessed here [Google Doc Submission](https://docs.google.com/document/d/14hXUTW-TxVFujGxfeL9fkO9iJ3jK5Oxc/edit?usp=sharing&ouid=100421826087392022828&rtpof=true&sd=true)

---

### Table of Contents
1. [Exercise #1 – JQ Patterns](#exercise-1--jq-patterns)  
2. [Exercise #2 – Jira & GitHub Integration](#exercise-2--jira--github-integration)  
3. [Exercise #3 – PR Count Scorecard](#exercise-3--pr-count-scorecard)  
4. [Exercise #4 – GitHub Workflow Troubleshooting](#exercise-4--github-workflow-troubleshooting)

---

## Exercise #1 – JQ Patterns

### 1(a) Extract current replica count  
**Jq Pattern**:  
```jq
.status.replicas
```
**Explanation**:  
Retrieves the integer value of the current replica count from a Kubernetes Deployment object.  

**OutPut**:  
```
1
```  
**Image Evidence**:    
![Alt text](images-clear/staus-replicas.png)

---

### 1(b) Extract deployment strategy  
**Jq Pattern**:  
```jq
.spec.strategy.type
```
**Explanation**:  
The leading . represents the root of the JSON object.  
.status moves into the status field of the Deployment object.  
.replicas then accesses the replicas field inside status, which holds the current replica count.  

**OutPut**:  
```
RollingUpdate
```
**Image Evidence**:  
![Alt text](images-clear/3.png)

---

### 1(c) Extract the “service” label of the deployment concatenated with the “environment” label of the deployment, with a hyphen (-) in the middle.  
**Jq Pattern**:  
```jq
.metadata.labels.service + “-” + .metadata.labels.environment
```
**Explanation**:  
Accesses the two label values and concatenates them into a single string.  

**OutPut**:  
```
authorization-production-gcp-1
```

**Image Evidence**:  

![Alt text](images-clear/4.png)

Image proof from local pc.

![Alt text](images-clear/5.png)

---

### 2 Extract all subtask issue IDs
**Jq Pattern**:  
```jq
[.fields.subtasks[].key]
```
**Explanation**:  
.fields.subtasks (array of subtasks) and extracts the key of each.  

**OutPut**:  
```
[
  "SAMPLE-3894",
  "SAMPLE-3895",
  "SAMPLE-3896",
  "SAMPLE-3897",
  "SAMPLE-3898",
  "SAMPLE-3899",
  "SAMPLE-3900",
  "SAMPLE-3902",
  "SAMPLE-3904",
  "SAMPLE-3901",
  "SAMPLE-3905",
  "SAMPLE-3906",
  "SAMPLE-3907"
]
```
**Image Evidence**:   

![Alt text](images-clear/6.png)

![Alt text](images-clear/7.png)

---

## Exercise #2 – Jira & GitHub Integration
### Steps Taken:  
1. **Signed Up to Port with this email. divine+port@solmateai.site.**
2. **Installed Port's GitHub app and authorized repos.**
  
   image below shows the installed getport github application.
![Alt text](images-clear/8.png)

3. **Created Jira project (Excercise2) with Scrum template (company-managed).**

   images below shows the created Jira project.  
   ![Alt text](images-clear/9.png)  

   ![Alt text](images-clear/10.png)  
   
4. **Installed Port Ocean Integration for Jira via Helm.**
  
   image below shows the installation instruction for Port Ocean Integration for Jira 
   ![Alt text](images-clear/11.png)

   image below shows the helm command for the Port Ocean Integrator deployment on Kubernetes.
   ![Alt text](images-clear/12.png)

   image below shows the Port Ocean Integrator pod running in Kubernetes 
   ![Alt text](images-clear/13.png)  

   image below shows evidence of the connected Jira and Github datasources 
   ![Alt text](images-clear/data-sources2.png)  

6. **Added relation Jira Issue → Repository.**
  
   image below shows the added relation btw Jira issues and GitHub repositories
   ![Alt text](images-clear/14.png)

7. **Created matching Jira components for repos.**

   images below show the components and the repositories with matching names
   ![Alt text](images-clear/15.png)
   
   ![Alt text](images-clear/16.png)

8. **Updated Jira integration mapping.**

   image below shows the Jira issue updated mapping.  
   ![Alt text](images-clear/17.png)

   image below shows the Audit Log to show that the mapping works  
   ![Alt text](images-clear/18.png)

   ![Alt text](images-clear/19.png)

---

## Exercise #3 – PR Count Scorecard 

1. **Added the aggregation property named openPrs**
   
   image below shows the added Aggregation property 
   ![Alt text](images-clear/20.png)

   Images below show the steps for the Aggregation property setup
   ![Alt text](images-clear/21.png)
   ![Alt text](images-clear/22.png)

2. **Added the scorecard logic to the Repository blueprint**
```jq
{ 
  "identifier": "open_prs_scorecard", 
  "title": "Open PRs per Repository", 
  "levels": [ 
    { 
      "color": "paleBlue", 
      "title": "Basic" 
    }, 
    { 
      "color": "bronze", 
      "title": "Bronze" 
    }, 
    { 
      "color": "silver", 
      "title": "Silver" 
    }, 
    { 
      "color": "gold", 
      "title": "Gold" 
    } 
  ], 
  "rules": [ 
    { 
      "identifier": "open_prs_gold", 
      "title": "Gold: < 5 Open PRs", 
      "level": "Gold", 
      "query": { 
        "combinator": "and", 
        "conditions": [ 
          { 
            "operator": "<", 
            "property": "open_prs", 
            "value": 5 
          } 
        ] 
      } 
    }, 
    { 
      "identifier": "open_prs_silver", 
      "title": "Silver: < 10 Open PRs", 
      "level": "Silver", 
      "query": { 
        "combinator": "and", 
        "conditions": [ 
          { 
            "operator": "<", 
            "property": "open_prs", 
            "value": 10 
          } 
        ] 
      } 
    }, 
    { 
      "identifier": "open_prs_bronze", 
      "title": "Bronze: < 15 Open PRs", 
      "level": "Bronze", 
      "query": { 
        "combinator": "and", 
        "conditions": [ 
          { 
            "operator": "<", 
            "property": "open_prs", 
            "value": 15 
          } 
        ] 
      } 

    } 

  ] 

} 
  ```
   
   image below shows the scorecard for the repository EagleEye with 1 open PR 
   ![Alt text](images-clear/23.png)
    
   image below shows the scorecard for the repository public-apis with 6 open PR 
   ![Alt text](images-clear/24.png)
   
   ![Alt text](images-clear/25.png)


## Exercise #4 – GitHub Workflow Troubleshooting

### Step 1. Verify Action Backend Configuration 

**Organization, Repository, and Workflow Name:** 
Double-check that the self-service action in Port is configured with the correct GitHub organization, repository, and workflow file name. Any typo or mismatch will most likely prevent the workflow from being triggered. This is a common cause and will result in the action being stuck in progress with no activity in GitHub. 

**Workflow Location:** 
Ensure the workflow file exists in the .github/workflows/ directory of the specified repository and branch. 

---

### Step 2. GitHub App Installation 

**App Installation:** 
Confirm that Port’s GitHub App is installed in the correct GitHub organization and on the relevant repository. 

**Permissions:** 
The GitHub App must have the necessary permissions (Actions, Pull Requests, Contents, etc.) and be installed on the repository where the workflow resides. 
 
---

### Step 3. Workflow Trigger Configuration 

**workflow_dispatch Trigger:** 
The workflow must be configured to use the workflow_dispatch trigger. Without this, it cannot be triggered remotely by Port. 

**Branch Existence:** 
If specifying a branch via the ref key, customer has to ensure the workflow file exists in the default branch as well, due to GitHub’s requirements. 

---

### Step 4. Secrets and Authentication 

**Port Credentials:** 
Ensure the GitHub repository contains the correct PORT_CLIENT_ID and PORT_CLIENT_SECRET as secrets, if required by your workflow. 

**GitHub Token:** 
If using a webhook invocation, verify that the GitHub token used has the necessary permissions and is correctly referenced in Port’s secrets. 

---

### Step 5. Logs and Error Messages 

**Check Port UI and Logs:** 
Look for any error messages in the Port UI or logs. Sometimes, errors such as “Got 404 while addressing github api, repo or workflow not found” indicate misconfiguration of org, repo, or workflow names. 

**GitHub Workflow Runs:** 
Check the Actions tab in the GitHub repository to see if any workflow runs were triggered or if there are any failed runs. 

---

### Step 6. Additional Checks 

**Action Organization/Repository:** 
If using templates or guides, ensure you have replaced all placeholder values (e.g., <GITHUB_ORG>, <GITHUB_REPO>) with your actual organization and repository names. 

**Secrets in Port:** 
Make sure all required secrets are set in Port (e.g., GitHub tokens, Port credentials). 
 
