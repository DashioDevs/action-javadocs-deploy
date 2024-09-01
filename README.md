# Deploy Javadoc to GitHub Pages

This GitHub Action automates the deployment of Javadoc documentation to GitHub Pages. It builds your Java project, generates Javadoc, and publishes it to a GitHub Pages branch.

## Features

- **Automatic Javadoc Generation**: Builds the project and generates Javadoc documentation.
- **Customizable Branch**: Publish Javadoc to a specified GitHub Pages branch.
- **JDK Configuration**: Supports multiple JDK versions and distributions.
- **Test Skipping**: Option to skip tests during the build process.
- **Branch Cleanup**: Option to clean up old branches before publishing.

## Inputs

### `GITHUB_TOKEN`
- **Description**: GitHub token used for repository access and authentication.
- **Required**: Yes

### `CLEANUP_BRANCH`
- **Description**: Whether to clean up old branches. Set to `'true'` to delete the old branch before publishing. Defaults to `'false'`.
- **Required**: No
- **Default**: `'false'`

### `BRANCH`
- **Description**: The name of the branch where the Javadoc documentation will be published. Defaults to `'gh-pages'`.
- **Required**: No
- **Default**: `'gh-pages'`

### `JAVA_VERSION`
- **Description**: The version of Java your project is using (e.g., 17).
- **Required**: Yes
- **Default**: `'17'`

### `JAVA_DISTRIBUTION`
- **Description**: The JDK distribution to use (e.g., `'adopt'`, `'zulu'`). Defaults to `'adopt'`.
- **Required**: No
- **Default**: `'adopt'`

### `SKIP_TESTS`
- **Description**: Whether to skip tests during the build process. Set to `'true'` to skip tests, `'false'` otherwise.
- **Required**: No
- **Default**: `'false'`

### `DOC_DIRECTORY`
- **Description**: The directory where the Javadoc documentation is generated. Defaults to `'target/reports/apidocs'`.
- **Required**: No
- **Default**: `'target/reports/apidocs'`

## Usage

To use this GitHub Action, create a workflow YAML file in your repository's `.github/workflows` directory.

### Example Workflow

Here’s an example workflow that builds the project, generates Javadoc, and publishes it to the `gh-pages` branch:

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
          CLEANUP_BRANCH: 'false'
```

### Example with Branch Cleanup

If you want to clean up old branches before publishing, set the CLEANUP_BRANCH input to 'true':

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
          CLEANUP_BRANCH: 'true'
```