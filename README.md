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
