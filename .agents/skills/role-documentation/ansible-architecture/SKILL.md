---
name: Ansible Architecture Rules
description: How to write andisble playbooks, roles and tasks following architecture rules
---
# Ansible Storybook Skill (Architecture Rules)

## 1. Domain separation

- All configuration is divided into **domains**
  - dns
  - certificates
  - crl
  - vpn
  - monitoring
  - etc

- Each domain is an independent bounded context.

---

## 2. Domain Playbook (Storybook entrypoint)

### 2.1 Responsibilities

A playbook MUST:

- NOT contain business logic
- ONLY orchestrate execution

Allowed responsibilities:
- 2.1.1 Orchestration of:
  - roles
  - task lists (include_tasks)

- 2.1.2 Definition of target scope:
  - hosts
  - groups

- 2.1.3 Execution of validation BEFORE any action:
  - validation task MUST be first executed step

---

## 3. Roles (Infrastructure definition)

### 3.1 Purpose

Roles define:
- infrastructure configuration rules
- reusable system components
- state definitions

### 3.2 Validation requirement

- Every role MUST include `validation.yaml` IF:
  - not all input variables have safe defaults
  - or external dependencies exist

- validation MUST be executed at role entry

---

## 4. Task Lists (Procedures / Pipelines)

### 4.1 Purpose

Task lists define:
- procedural workflows
- transformations
- data aggregation
- deployment steps

---

### 4.2 Requirements

- Every complex task list MUST include documentation:
  - `README.md`

- Task list MUST include `validation.yaml` IF:
  - it accepts input parameters without defaults

- Task list MUST be decomposed if large:
  - split into sub-task directories

---

### 4.3 Structure rule

If task list contains multiple logical units:

- MUST be placed in a dedicated directory

---

## 5. Validation rule (global)

- `validation.yaml` MUST be executed:
  - at start of every role
  - at start of every task list
  - at start of every playbook

- Validation is mandatory fail-fast mechanism

---

## 6. Default values handling rule (IMPORTANT)

If a task list defines **default values for input parameters**, then:

### 6.1 validation.yaml MUST contain initialization step

At the beginning of `validation.yaml`, default values MUST be set explicitly:

```yaml
# Set default values
# Установка значений по умолчанию
- name: set default values
  set_fact:
    ...
  when: skip_set_fact is not defined or not skip_set_fact
```

### 6.2 Execution model

There are TWO execution modes:

A. Playbook level execution (default behavior)
- Playbook calls validation WITHOUT skip_set_fact
- Default values ARE applied

```yaml
- name: Validate deploy prerequisites
  include_tasks: validation.yaml
```

B. Task list internal execution (strict validation mode)
- Task list MUST call validation with skip_set_fact: true
- Default values MUST NOT be applied
- Only validation is performed

```yaml
- name: Validate deploy prerequisites
  include_tasks: validation.yaml
  vars:
    skip_set_fact: true
```

6.3 Rule summary
- Playbook = applies defaults + validates
- Task list = validates only (no mutation of state)
- Default assignment MUST be centralized in validation.yaml
- skip_set_fact controls mutation vs validation-only mode

---

## 7. Directory structure standard

```text
ansible/
  modules/
    {{ module_name }}/

      playbooks/
        {{ playbook_name }}.yaml

      tasks/
        {{ task_list_name }}/
          README.md
          templates/
          task/
            # optional subtask decomposition
          main.yaml
          validation.yaml

      roles/
        {{ role_name }}/
          README.md
          tasks/
            main.yaml
            validation.yaml
          # standard Ansible role structure allowed
```

---

## 8. Execution hierarchy

```
Playbook (storybook)
  ├── validation.yaml
  ├── roles execution (state layer)
  └── tasks execution (process layer)
        ├── validation.yaml
        └── workflow steps
```

## 9. Key principles
- Playbooks = orchestration only
- Roles = infrastructure state
- Tasks = procedural workflows
- Validation = mandatory entry gate everywhere
- No business logic inside playbooks
- No implicit assumptions without validation