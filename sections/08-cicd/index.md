---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD

Mete.io will use Github Actions for the Continuous Integration (CI) workflow, this can be achieved in combination with unittest and Poetry.

This helps pinpoint integration issues early, allows for reproducible and consistent building and testing across different environments and can be used to run periodic tests to address changes in dependencies. 

It also reduces human error by removing repetitive tasks and helping the team focus on more creative activities (developing new features, fixing bugs etc.).

Github Actions is well integrated with Github repositories avoiding added complexity of implementing an external Continuous Integration (CI) software.

The CI pipeline is automatically activated on every push and pull (for merge) request to the main branch. 

Each CI run performs the following steps:

- Repository checkout, source code is cloned using Git;

- Environment setup, Python is installed on the runner according to the build matrix;

- Dependency installation, project dependencies are restored using Poetry;

- Automated Test execution with unittest;

- Coverage reporting, test coverage can be computed (e.g. via coverage.py as a dev dependency) and reported to show how much of the codebase is executed during automated tests.

A build matrix is used to test the application across:

- Operating systems (Windows 10 and 11);

- Python versions (3.10, 3.11, 3.12, 3.13, 3.14).

Each combination of system-version would be executed independently in parallel, so that failures could be detected in specific environments without blocking the entire pipeline.

## Continuous Delivery (CD)

Successful builds on the main branch can activate:

- version checks;

- packaging of the application using Poetry;

- publication of release artefacts to PyPI.

Release jobs can be configured to run only when:

- a version tag is created;

- or a release branch is merged.

This approach ensures that every released artefact has passed the full set of automated tests.