---
layout: post
title: "SDLC Stages"
date: 2026-07-18    
tags: design ai
---

## SDLC Stages, Roles, and Outputs — Reference

> A consolidated reference mapping each stage of the Software Development Life Cycle (SDLC) to its primary roles, responsibilities, and expected outputs. Derived and synthesized from the sources listed below; not a direct translation.

- Shruti Soni, ["Essential Stages of SDLC & Key Roles That Drive Success"](https://www.linkedin.com/pulse/essential-stages-sdlc-key-roles-drive-success-shruti-soni--xh5df/), LinkedIn Pulse
- GeeksforGeeks, ["Software Development Life Cycle (SDLC)"](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/)
- Dila Leynart, ["Software Development Life Cycle (SDLC): Process, Steps, Team Roles, and Common Alternative Models"](https://medium.com/@dilaleynartl/software-development-life-cycle-sdlc-process-steps-team-roles-and-common-alternative-models-e53740c66ab4), Medium
- GitHub Resources, ["What is SDLC?"](https://github.com/resources/articles/what-is-sdlc)
- resourceguruapp, [Project team roles and responsibilities](https://resourceguruapp.com/blog/project-management/project-team-roles-and-responsibilities)

---

## Stage-by-stage reference table

| Stage | Primary Roles | Key Responsibilities | Typical Outputs |
|---|---|---|---|
| **Planning** | Project Manager, Project Sponsor, Business Analyst | Feasibility analysis, cost estimation, scheduling, resource planning; sponsor secures budget and staffing; PM/BA define scope and align stakeholders | Project plan, feasibility report, resource/budget plan |
| **Requirement Analysis** | Business Analyst, Product Manager, Customer Representatives, Users | Gather and document functional/non-functional requirements; translate business needs into specifications | Software Requirements Specification (SRS) |
| **Design** | Software/System Architects, UI/UX Designers, System Analysts | Define architecture, tech stack, database and module structure (high-level design); define component logic, APIs, data structures (low-level design); shape UX | Design Document Specification (DDS), architecture diagrams |
| **Development** | Developers (Frontend, Backend, Full-Stack, Mobile, API) | Write code per approved design; code reviews; unit testing; version control management | Source code, executable application/build artifacts |
| **Testing** | QA Engineers, Developers (unit testing), Automation Teams | Define test strategy and cases; run unit, integration, system, regression, and UAT testing | Test plan, test cases, test/defect reports |
| **Deployment** | DevOps Engineers, Release Managers, System Administrators | Production environment setup, deployment (increasingly via CI/CD pipelines), smoke testing | Deployed/released application, deployment pipeline config |
| **Maintenance** | Support Engineers, Developers, Product Teams | Bug fixes, performance tuning, updates, feature enhancements, monitoring | Patches/updates, incident/maintenance logs |

---

## Notes on role overlap and framing differences

- **Planning ownership**: the GeeksforGeeks source frames Planning as owned jointly by project managers, senior engineers, and stakeholders, while the supplementary Ubiminds source is more specific — it splits this into the Project Manager/Business Analyst (scope, stakeholder alignment) and the Project Sponsor (budget, staffing) as a distinct role. This table follows the more specific split.
- **DevOps/DevSecOps as cross-cutting**: the GitHub Resources article emphasizes that DevOps (and DevSecOps) roles aren't confined to the Deployment stage — they represent ongoing collaboration between developers, IT operations, and security across the whole lifecycle, not a single handoff point.
- **Product ownership spans stages**: Product Managers appear in both Requirement Analysis and as a lifecycle-spanning role (alongside analysts, test engineers, and support teams) depending on the source — treat "Product Manager" as present from Requirements through Maintenance rather than confined to one box in the table.
- **QA vs. developer testing**: unit testing is commonly done by developers themselves, with QA Engineers and Automation Teams owning integration/system/regression/UAT — the Testing row above reflects that split rather than assigning all testing to one role.


