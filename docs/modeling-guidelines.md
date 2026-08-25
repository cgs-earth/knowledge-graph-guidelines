# CGS Knowledge Graph Guidelines

This repository defines the architecture, namespace policy, governance practices, and publication requirements for ontologies and knowledge graphs developed or integrated by CGS.


```mermaid
flowchart TB
    standards["External standards"]
    domains["Agency and community domain ontologies"]
    core["CGS core ontologies"]
    alignments["Alignment ontologies"]
    projects["Project ontologies"]
    profiles["Application profiles and SHACL shapes"]
    data["Instance-data graphs"]

    standards --> domains
    standards --> core
    domains --> alignments
    core --> alignments
    domains --> projects
    core --> projects
    alignments --> projects
    projects --> profiles
    domains --> data
    projects --> data
```
