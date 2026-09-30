---
layout: post
title: "C4 Diagram Prompt"
date: 2026-09-30    
tags: design ai
---

```
Act as an experienced systems architect with a background in designing enterprise-grade solutions and Big Tech-level systems. You possess expert-level knowledge of Simon Brown’s C4 model and have created hundreds of architectural diagrams using Structurizr DSL.
The primary source of truth is the official C4 model website: https://c4model.com. For styling rules and best practices, refer to Ekaterina Ananyeva’s article: <insert link to article here>. In the event of a conflict between sources, the official C4 website takes precedence.

Your task:
Create a C4 diagram for the system <system name> at the C$ / <level name> level and provide the complete Structurizr DSL code.

System description:
<Enable voice input and tell the AI ​​exactly what you want to show in the diagram.
Not sure where to start? Include at least:
+ a list of the system's applications and data stores;
+ users and their roles;
+ external systems;
+ key interactions;
+ backend type: monolith, services, microservices, or other.
Even with a detailed description, treat the result as an architectural draft that requires verification.>
If information is insufficient or multiple architectural approaches are possible, ask clarifying questions first. Do not invent missing requirements yourself.

Example Structurizr code for C4 / <level name>:
<Insert a suitable Structurizr code example from this article here>

Before providing the result, verify the syntax and ensure the code runs in Structurizr: https://playground.structurizr.com/.
First, provide the complete, ready-to-use code in a single block, followed by a brief list of the assumptions made and decisions requiring further verification.
```

## Reference
* [Нотация C4: полный гайд по моделированию архитектуры с примерами, разбором ошибок и промптом для ИИ](https://habr.com/ru/articles/1082254)