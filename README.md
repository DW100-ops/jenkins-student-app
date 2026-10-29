# Jenkins Student Application

This repository contains a simple Python application used to demonstrate a full CI/CD workflow in Jenkins.

## Contents

- `app.py`: Core application logic containing the `add` function.
- `test_app.py`: Unit test suite executing tests via `unittest`.
- `Jenkinsfile`: Declarative CI pipeline configuration automating Checkout, Build, Test, and Packaging stages.

## CI/CD Pipeline

The automated Jenkins pipeline executes four primary stages:

1. **Checkout**: Source code retrieval from Git.
2. **Build**: Syntax validation using `py_compile`.
3. **Test**: Unit test execution via `unittest`.
4. **Package**: Compresses application files into `app-package.tar.gz` and archives artifacts.
