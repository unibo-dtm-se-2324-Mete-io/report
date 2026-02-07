---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

## User installation

Since Mete.io would be distributed as a Python package via PyPI, deployment focuses on user-side installation.

### Prerequisites

To run Mete.io, the user would need to have:

- Windows 10 or higher

- Python 3.10 or higher

- pip, the Python package installer (included with Python)

Python can be installed by downloading the official installer from the Python website (python.org).
During installation, the option “Add Python to PATH” should be enabled to allow execution from the command line.

### Installation steps

Mete.io would be installed directly from PyPI using pip.

1. Open Command Prompt or PowerShell

2. Run the following command:

    pip install mete-io

This command would download the Mete.io package from PyPI, automatically install all required dependencies (e.g. Kivy) and ensure version compatibility based on package metadata.

### Running the application

After installation, the application could be run with the command (if Python is included in the system PATH):

    mete-io

Alternatively, the application could be run as a Python module:

    python -m mete-io

No manual configuration is needed.

## Server-side installation

Mete.io does not require installation server-side, it runs on the user’s device and all the data is retrieved from Open-Meteo.

