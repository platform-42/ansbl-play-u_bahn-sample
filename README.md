# 🚉 Neo4j Railway Graph Loader (Ansible Playbook)

This Ansible playbook automates the process of loading **stations** (nodes) and **tracks** (relationships) into a **Neo4j** graph database.  
It is designed to work with the custom Neo4j Ansible collection:
- `neo4j.vertex`        - create a node
- `neo4j.edge`          - create a relationship
- `neo4j.query_read`    - query created graph
- `neo4j.graph_reset`   - reset graph in database (cleanup)
- `neo4j.label`         - assign additional label(s) to a node
- `neo4j.constraint`    - create unique constraint in node property

---

## 🧩 Overview

The playbook reads YAML or JSON definitions of railway infrastructure (stations and tracks) and applies them declaratively to a Neo4j database.

**Example use case:**
- Import a set of train stations and the tracks connecting them.
- Keep the graph model consistent with a source of truth file.
- Easily reapply or modify data using idempotent Ansible runs.

---

## 🏗️ Repository Structure

```text
├── u_bahn.yml                  # main playbook
├── u_bahn.sh                   # execute main playbook -> load u_bahn graph
├── query.yml                   # shortest path playbook from source -> destination
├── query.sh                    # execute path playbook
|
├── tasks/
│       ├── edges/*.yml         # tasks for adding tracks
│       ├── vertices/*.yml      # tasks for adding stations
│       ├── dependencies/*.yml  # tasks for installing dependencies
│       └── database/*.yml      # tasks for resetting graph database
│
├── vars/
│       ├── edges/*.yml         # track definitions
│       ├── vertices/*.yml      # station definitions
│       └── settings 
│                  ├── cloud
│                  │       └── settings.yml      # AURA credentials
│                  └── local
│                          └── settings.yml      # Localhost credentials
├── hosts/
│       └── hosts.yml                            # local host definitions
|
└── README.md                   # You are here
```

---

## Steps before usage ...

1. have python3 installed
2. have ansible installed
3. have NEO4J installed (local on your PC) or create NEO4J Aura account (cloud)
4. Inspect which python interpreter you are using and adjust `hosts/hosts.yml` with right python3 interpreter
    * `which python3`
    * adjust `ansible_python_interpreter` with what `which` returned

Keep in mind, the software was developed on a Mac. 
Please specify a Linux path for `ansible_python_interpreter`