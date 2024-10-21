# Build container reusable workflow details

> Build container with Maven.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v4` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- The Artifact Name is retrieved from `<artifactId>` in the `pom.xml` file using SED[sed] to be used as part of the [docker][docker] tag
- If the workflow is triggered by release, the tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [revision][revision] flag via a Docker ARG variable.
- The container image name is formulated as `<artifact-name>:<revision>_<git-short-sha>`. If the workflow is not triggered by a release, we remove revision from the tag: `<artifact-name>:<git-short-sha>`.
- The container is built using [docker][docker] build directly.

[checkout]: https://github.com/marketplace/actions/checkout
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[sed]: https://manpages.ubuntu.com/manpages/jammy/man1/sed.1.html
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions
[docker]: https://docs.docker.com/build/