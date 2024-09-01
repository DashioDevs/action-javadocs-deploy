### 📘 Introduction

This GitHub Action automates the deployment of Javadoc documentation to GitHub Pages. It builds your Java project, generates Javadoc, and publishes it to a specified branch, typically `gh-pages`.

### ✨ Features

- **Automatic Javadoc Generation**: Automatically builds the project and generates Javadoc documentation.
- **Customizable Branch**: Allows publishing of Javadoc to a specified branch (default is `gh-pages`).
- **Flexible JDK Configuration**: Supports multiple JDK versions and distributions, allowing for easy customization.
- **Optional Test Skipping**: Configurable option to skip tests during the build process.
- **Branch Cleanup**: Ability to clean up old branches before publishing, ensuring a fresh deployment environment.

### ⚙️ Inputs

The following inputs can be configured for this action:

#### `GITHUB_TOKEN`
- **Description**: GitHub token used for repository access and authentication.
- **Required**: Yes

#### `BRANCH`
- **Description**: The branch where the Javadoc documentation will be published. Defaults to `'gh-pages'`.
- **Required**: No
- **Default**: `'gh-pages'`

#### `BRANCH_CLEANUP`
- **Description**: Whether to clean up old branches before publishing. Set to `'true'` to delete the old branch. Defaults to `'false'`.
- **Required**: No
- **Default**: `'false'`

#### `JAVA_VERSION`
- **Description**: The version of Java your project is using (e.g., `17`).
- **Required**: Yes
- **Default**: `'17'`

#### `JAVA_DISTRIBUTION`
- **Description**: The JDK distribution to use (e.g., `'adopt'`, `'zulu'`). Defaults to `'adopt'`.
- **Required**: No
- **Default**: `'adopt'`

#### `SKIP_TESTS`
- **Description**: Whether to skip tests during the build process. Set to `'true'` to skip tests.
- **Required**: No
- **Default**: `'false'`

#### `DOC_DIRECTORY`
- **Description**: The directory where the Javadoc documentation is generated. Defaults to `'target/site/apidocs'`.
- **Required**: No
- **Default**: `'target/site/apidocs'`

### 🚀 Usage

To use this GitHub Action, create a workflow YAML file in your repository's `.github/workflows` directory.

#### Example Workflow

Below is an example workflow that builds the project, generates Javadoc, and publishes it to the `gh-pages` branch:

```yaml
name: Deploy Javadoc to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy-javadoc:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the repository
        uses: actions/checkout@v4

      - name: Deploy Javadoc
        uses: DashioDevs/action-javadocs-deploy@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          JAVA_VERSION: '17'
          JAVA_DISTRIBUTION: 'adopt'
          SKIP_TESTS: 'false'
          DOC_DIRECTORY: 'target/site/apidocs'
          BRANCH: 'gh-pages'
          BRANCH_CLEANUP: 'false'
```


#### Example with Branch Cleanup

To clean up old branches before publishing, set the `BRANCH_CLEANUP` input to 'true':

```yaml
name: Deploy Javadoc to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy-javadoc:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the repository
        uses: actions/checkout@v4

      - name: Deploy Javadoc
        uses: DashioDevs/action-javadocs-deploy@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          JAVA_VERSION: '17'
          JAVA_DISTRIBUTION: 'adopt'
          SKIP_TESTS: 'false'
          DOC_DIRECTORY: 'target/reports/apidocs'
          BRANCH: 'gh-pages'
          BRANCH_CLEANUP: 'true'
```

### 📄 License
This project is licensed under the Apache License 2.0 - see the [LICENSE file](https://github.com/DashioDevs/action-javadocs-deploy/blob/main/LICENSE) for details.
