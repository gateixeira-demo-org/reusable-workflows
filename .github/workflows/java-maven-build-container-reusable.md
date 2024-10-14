# Build container reusable workflow details

> Build container with Maven using [Quarkus framework][quarkus].

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v3` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- If the workflow is triggered by release, the tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [SED][sed] command.
- The container image name is formulated from repository context using the [SED][sed] command.
- The container is built using the [`quarkus-maven-plugin`][quarkusmavenplugin] part of the Quarkus Maven wrapper using the following parameters:
  - `-Pnative`
  - `-Dquarkus.container-image.build=true`
  - `-Dquarkus.container-image.tag=latest`
  - `-Dquarkus.container-image.group=${{ github.repository_owner }}`
  - `-Dquarkus.container-image.name=${{ env.container_image_name }}`
- Finally a file listing overview of the runner workspace is printed to the Actions workflow log.

[checkout]: https://github.com/marketplace/actions/checkout
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[quarkusmavenplugin]: https://quarkus.io/guides/quarkus-maven-plugin
[sed]: https://manpages.ubuntu.com/manpages/jammy/man1/sed.1.html
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions
[quarkus]: https://quarkus.io/
