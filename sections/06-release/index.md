---
title: Release
has_children: false
nav_order: 7
---

# Release

The project would produce **one artefact**, a Python application package containing the Mete.io code and its runtime dependencies.

The source code is hosted on GitHub for development, while the packaged artefact would be distributed via **PyPI**. PyPI was chosen because it is the standard and most appropriate repository for Python software and it integrates with pip and Poetry.

Mete.io would use **Poetry** to handle dependency management, packaging and release of the software to PyPI. This would allow for a better user installation experience because the needed libraries (e.g. kivy) would be automatically installed and managed by Poetry, as long as the .toml files have been properly defined. 

Releases could be performed manually or automatically using CI/CD pipelines (GitHub Actions).

The steps for manual release would be:

1. Update the version number in pyproject.toml

2. Commit the version change:

    git commit -m "chore(release): bump version to X.Y.Z"

3. Create a Git tag:

    git tag vX.Y.Z

    git push origin vX.Y.Z

4. Build and publish the package:

    poetry build

    poetry publish --username __token__ --password $PYPI_TOKEN

In an automated setup, the same steps would be executed by a GitHub Actions workflow after a merge into the main branch or after pushing a version tag.

## Choice of the license

The licence choice for the source code was **Apache License 2.0**.

The reason behind this choice was because it allows redistribution and modification of the original software while forcing authors of derivative work to indicate meaningful changes done to the software. 

It is also a balance between the very permissive MIT License and the GNU (GLPv3, LGLPv3, GLP with linking exceptions) Licenses that are too restrictive and may create licensing conflicts with the Kivy license (MIT License).

For the documentation the choice was **Creative Common License CC-BY**, allowing to distribute, adapt and build upon as long as the creators are credited. 

This choice was made to provide the possibility of derivative work but still being able to be properly credited for the work done.

## Choice of the versioning schema

Mete.io followed the Semantic Versioning (SemVer) schema with the format X.Y.Z with X indicating the major version (incompatible or breaking changes), Y the minor one (backward-compatible feature additions) and Z the patch (backward-compatible bug fixes). X.Y.Z can also be represented as MAJOR.MINOR.PATCH. 

This choice was made because it provides an easy overview of the modification of the software, also Poetry strongly encourages the use of SemVer. 

An example of version during early development would be 0.1.1 and once officially released 1.0.0.

The project will not feature multiple artefacts but in case of an increased complexity of the software needing multiple artefacts the versioning would follow the same versioning schema but it may not align.

This may be caused by a different need for immediate patch or a different release of a minor feature.

**Creating a new version**

A new version would be created following these rules:

PATCH increment:

- bug fixes;

- documentation fixes;

- internal refactoring without functional changes.

MINOR increment:

- new features;

- new optional indicators;

- backward-compatible API changes.

MAJOR increment:

- breaking changes;

- removal or modification of existing behaviour.

Each release would correspond to:

- a Git tag (vX.Y.Z);

- a GitHub Release;

- a published package on PyPI.

A new **release branch** should be created from the develop branch once the team starts preparing the release version (in the meantime the team can start working on the next version, new features etc.), once finished its changes should be merged into main and develop. 