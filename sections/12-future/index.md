---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

The most important direction of future work would contain practical implementation of all detailed concepts, including writing tests, artifact source code, configuring CI/CD with GitHub Actions, the Poetry .toml files, etc.

Following are some other weaknesses and future developments not yet solved in the report:

## Mobile Support

In the initially written list of requirements, the application was said to support both Windows and Android (of the newer OS versions), but later the scope was reduced to focus on the desktop users to align the release and deployment logic in a simpler way.

In the future the software should plan and execute releases for Android, by packaging the artifact differently and releasing them to Play Store.

## Dependency on External APIs

Mete.io relies entirely on third-party public weather APIs, API downtime or changes in API output may cause temporary loss of functionality. The output changes are partially mitigated by API adapters.

This is an intended behaviour, but it is important to point out.

## Limited Persistence
- User data (previously searched locations) is stored locally using simple storage mechanisms.

- There is no synchronization across devices (since there is no account authorization).

- Data is lost if the application is uninstalled or the local storage is manually cleared.

In the future user accounts with persistent location data and secondary indicator preferences could be implemented, but it would require a server for the user to connect to, so it would become a distributed system. More simply, manual user data exporting and importing could be implemented.

## Testing extension and coverage analysis

Testing examples provided were not only not practically implemented, but also non-exhaustive. Tests will need to cover all components and account for all the requirements and their acceptance criteria. Test coverage will need to be monitored, but it’s not enough, the quality of the tests will also need to be evaluated and all edge cases should be considered.
