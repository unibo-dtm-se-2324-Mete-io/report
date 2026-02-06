---
title: Development
has_children: false
nav_order: 5
---

# Development

## DVCS

Git and GitHub were used for version control.

The convention of the usage of branches followed the one taught at the Software Engineering course with the creation of a main branch, a develop branch and from it - subsequent ones for each feature (named “feature/section-N”). 

There was a mistake from the member Morello that committed the first section “01-Concept” directly on main, but it has been long fixed.

The Mete.io application used the “Conventional Commit specification” with the following structure:

**< type >** [optional scope]: **< description >**

[optional body]

[optional footers]

The type element followed the semantics of: fix (e.g. patch a bug), feat (new feature), BREAKING CHANGE (or the usage of “!” after the type) and types based on angular conventions (e.g. docs, test, chore).

For the report repository, since the contents were written in markdown, the team considered the report itself to be documentation (for the entire project scope with possible artifacts), and used the “docs:” commit type for sections content, and “fix:” for corrections. 

The team is aware that the report context could be considered a feature with the “feat:” commit type, but followed the previous interpretation. 

The description element described with a short sentence the effect of the commit and used the infinite form of verbs.

 ## Implementation details

**Network protocol** (HTTPS)

The HTTPS protocol is used to handle communications with the Open-Meteo API.

It is used to ensure confidentiality and integrity of in-transit data and it encrypts the data to avoid packet sniffing.
More complex protocols (e.g. WebSockets, gRPC) were unnecessary, as the application does not require real-time streaming or bidirectional communication.

**Data format** (JSON)

JSON is the format used by Open-Meteo APIs, so it was the choice to represent data. It is also widely supported by Python and its standard libraries.

**Data access**

Mete.io stores previously searched locations locally as key-value pairs.

When the application starts the stored locations are retrieved to show suggestions. 

When a new location is searched the location is saved for future reuse.

A full database (SQL or NoSQL) was not adopted because of minimal data volume, no concurrent access and simple persistence requirements.

**Authentication**

No API keys are required for the free subscription tier of Open-Meteo.

**Authorization**

There is no need for authorization because the application is single-user and there is no need for role attribution, also the only protected data that could be exposed is related to the coordinates of the user that are stored in the user’s local storage. 


## Technological details

**Language** (Python)

Python was chosen because of the familiarity during the study course and because it has strong support for testing, automation, and APIs.

**GUI framework** (Kivy)

Kivy is an open source software library that allows the development of graphical applications using Python only. The choice to use Kivy was made because it was studied during the course and the relatively small quantity of user interface needed for the Mete.io project.

**HTTP client** (requests)

The requests library is widely adopted and well documented and provides a simple and expressive API that integrates naturally with JSON-based REST APIs.

**Testing** (unittest)

Unittest  is a built-in library for writing tests in Python, it was chosen because it is included in the Python standard library and seems to fit the complexity level of the project.

**Continuous Integration** (GitHub Actions)

GitHub Actions was chosen because it's free for FOSS, it integrates directly with the repository and it allows continuous build, test and deployment.

**External dependency**:

Public weather API (Open-Meteo)

The Open-Meteo API was chosen because the project needed external reliable weather data that could be used and it was a free solution.