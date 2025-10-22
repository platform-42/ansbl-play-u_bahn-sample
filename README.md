# 🚉 Neo4j Railway Graph Loader (Ansible Playbook)

This Ansible playbook automates the process of loading **stations** (nodes) and **tracks** (relationships) into a **Neo4j** graph database.  
It is designed to work with the custom Neo4j Ansible collection (e.g. `neo4j.vertex`, `neo4j.edge`, `neo4j.query_read`, and `neo4j.cleanup` modules).

---

## 🧩 Overview

The playbook reads YAML or JSON definitions of railway infrastructure (stations and tracks) and applies them declaratively to a Neo4j database.

**Example use case:**
- Import a set of train stations and the tracks connecting them.
- Keep the graph model consistent with a source of truth file.
- Easily reapply or modify data using idempotent Ansible runs.

---

## 🏗️ Repository Structure

├── u_bahn.yml                  # main playbook
├── u_bahn.sh                   # execute main playbook -> load u_bahn graph
├── query.yml                   # shortest path playbook from source -> destination
├── query.sh                    # execute path playbook
|
├── tasks/
│       ├── edges/*.yml         # tasks for adding tracks
│       ├── vertices/*.yml      # tasks for adding stations
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
|
└── README.md                   # You are here

---

## before usage ...

have python3 installed
have ansible installed
have NEO4J installed (if localhost)

* pip3 install neo4j
* pip3 install regex

Inspect which python interpreter you are using and adjust hosts/hosts.yml with right python3 interpreter

* which python3
* adjust ansible_python_interpreter with path of witch python3

Keep in mind, the software was developed on a Mac. 
Please specify a Linux path for ansible_python_interpreter