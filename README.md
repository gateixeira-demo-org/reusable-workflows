# Reusable Workflows Repository

This repository contains a collection of reusable GitHub Actions workflows designed to streamline CI/CD processes for various languages and frameworks. Each workflow is designed to be easily integrated into your projects.

## Workflows

### Java Maven Workflows

#### Java Maven JUnit Test Reusable Workflow
- **File**: `java-maven-junit-reusable.yml`
- **Description**: This workflow runs JUnit tests for a Java Maven project.
- **Usage**:
  ```yaml
  jobs:
    test:
      uses: ./.github/workflows/java-maven-junit-reusable.yml
      with:
        runner: ubuntu-latest
        java-version: '11'
  ```

#### Java Maven Build Package Reusable Workflow
- **File**: `java-maven-build-package-reusable.yml`
- **Description**: This workflow builds a package from a Java Maven project.
- **Usage**:
  ```yaml
  jobs:
    build:
      uses: ./.github/workflows/java-maven-build-package-reusable.yml
      with:
        runner: ubuntu-latest
        java-version: '11'
  ```

### Node.js Workflows

#### NodeJS npm Test Reusable Workflow

- **File**: `nodejs-npm-test-reusable.yml`
- **Description**: This workflow runs tests for an NPM-based Node.js project.
- **Usage**:
  ```yaml
  jobs:
    test:
      uses: ./.github/workflows/nodejs-npm-test-reusable.yml
      with:
        runner: ubuntu-latest
        node-version: '19'
  ```

#### NodeJS npm Build Package Reusable Workflow

- **File**: `nodejs-npm-build-package-reusable.yml`
- **Description**: This workflow builds a package from an NPM-based Node.js project.
- **Usage**:
  ```yaml
  jobs:
    build:
      uses: ./.github/workflows/nodejs-npm-build-package-reusable.yml
      with:
        runner: ubuntu-latest
        node-version: '19'
  ```

## How to Use a Reusable Workflow

To use any of these reusable workflows in your project, reference the appropriate workflow file in your GitHub Actions configuration file (`.github/workflows/your-workflow.yml`). Make sure to specify the required inputs as shown in the examples above.