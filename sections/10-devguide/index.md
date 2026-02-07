---
title: Developer guide
has_children: false
nav_order: 11
---

# Developer Guide

This guide explains how a new developer can join the team and start contributing to the project following the team’s conventions.

## Project overview

Mete.io is a Python-based desktop weather application built with Kivy GUI, Poetry for dependency management and packaging, and unittest for testing. The architecture follows a layered design (UI → Application → Domain → Infrastructure).

## Organizational information

The team can be contacted via email and issues can be reported using the “issues” panel of the GitHub repository.

The report documentation is in the following repository:
 
https://github.com/unibo-dtm-se-2324-Mete-io/report

Future artifact repository:

https://github.com/unibo-dtm-se-2324-Mete-io/artifact

## Development conventions

**Branching**

Branching follows GitFlow:

- main - production-ready releases

- release - release preparation
- develop - ongoing development
- feature/section-N - new feature development
- hotfix/name - urgent fixes

Feature branch creation example:

	git checkout -b “feature/section-1”

**Commits**

Commits follow Conventional Commits of the following format:

    <type>[optional scope]: <description>
    [optional body]
    [optional footer(s)]

Report commit commands example:
	
	git add .
	git commit -m “type: description”
    git push

Report commit message examples:

    docs: update section-N
    fix: change forecast accuracy threshold

**Merges**

Section branches (feature/section-N) must be merged into develop once finished and then deleted.

Merge example:

	git checkout develop
	git merge feature/section-N

## Development environment

**Common prerequisites**

- git
- optional: GitHub GUI
- optional: VSCode

**Report development**

Cloning the repository:

    git clone https://github.com/unibo-dtm-se-2324-Mete-io/report.git

**Future artifact development**

Prerequisites:

- Python 3.10 or higher
- Poetry

Cloning the repository:

    git clone https://github.com/unibo-dtm-se-2324-Mete-io/artifact.git

Installing dependencies:

	poetry install