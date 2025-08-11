# Port Support Engineer Assignment

**Candidate:** Asomugha Divine  
**Date:** 11/08/2025  

### Table of Contents
1. [Exercise #1 – JQ Patterns](#exercise-1--jq-patterns)  
2. [Exercise #2 – Jira & GitHub Integration](#exercise-2--jira--github-integration)  
3. [Exercise #3 – PR Count Scorecard](#exercise-3--pr-count-scorecard)  
4. [Exercise #4 – GitHub Workflow Troubleshooting](#exercise-4--github-workflow-troubleshooting)

---

## Exercise #1 – JQ Patterns

### 1(a) Extract current replica count
```jq
.spec.replicas
```
**Explanation**: Retrieves the integer value of the current replica count from a Kubernetes Deployment object.

![Alt text](images/1.png)

![Alt text](images/2.png)

---

### 1(b) Extract deployment strategy
```jq
.spec.strategy.type
```
**Explanation**: Retrieves the deployment strategy type (e.g., RollingUpdate or Recreate).

![Alt text](images/3.png)

---

### 1(c) Extract the “service” label of the deployment concatenated with the “environment” label of the deployment, with a hyphen (-) in the middle.
```jq
.metadata.labels.service + “-” + .metadata.labels.environment
```
**Explanation**: Accesses the two label values and concatenates them into a single string. 

![Alt text](images/4.png)

Image proof from local pc.

![Alt text](images/5.png)

---

### 2 Extract all subtask issue IDs
```jq
[.fields.subtasks[].key]
```
**Explanation**: .fields.subtasks (array of subtasks) and extracts the key of each.

![Alt text](images/6.png)

![Alt text](images/7.png)

---

## Exercise #2 – Jira & GitHub Integration

