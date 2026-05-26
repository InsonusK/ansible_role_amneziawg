---
name: Ansible role documentation
description: How to write documentation for ansible role
---

# When to use this skill
- You have change ansible role
- You need write documentation for ansible role

# How to use it
1. All steps of task must have comments in English and Russian and describe what is happening in this step. English comments could be skip if the step is self-describing, but Russian comments are required for all steps.
2. All parameters in defaults/*.yml must have comments in English and Russian describing what this parameter is for. 
If any parameters is used in tasks/*.yml or templates/*.j2 but not defined in defaults/*.yml, you must add description of this parameters to documentation. You add information about this parameters to documentation in ./docs. You can use [template](./templates/readme-template.md.j2) for this.
2. If you add new input parameters to role, you must add description of this parameters to documentation. You can use [template](./templates/readme-template.md.j2) for this.