# Publish container reusable workflow details

> Publish container to GitHub Container Registry using Maven with [Quarkus framework][quarkus].

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v3` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- The tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [SED][sed] command.
- The [GitHub Container Registry (GHCR)][containerregistry] URL and container image name are constructed from available repository context using the [SED][sed] command.
- The container image name is formulated from repository context using the [SED][sed] command.
- Logging into the GitHub Container Registry is done using the [Docker Login][dockerlogin] action. The `docker/login-action@v2` uses the following environment variables to authenticate:
  - `registry: ${{ env.container_registry }}`
  - `username: ${{ github.actor }}`
  - `password: ${{ secrets.GITHUB_TOKEN }}`
- The container is built and published using the Maven wrapper part of the Quarkus framework by using the following parameters:
  - `-Pnative`
  - `-Dquarkus.container-image.build=true`
  - `-Dquarkus.container-image.push=true`
  - `-Dquarkus.container-image.registry=${{ env.container_registry }}`
  - `-Dquarkus.container-image.tag=${GITHUB_REF#refs/tags/}`
  - `-Dquarkus.container-image.group=${{ github.repository_owner }}`
  - `-Dquarkus.container-image.name=${{ env.container_image_name }}`
  - `-Dquarkus.jib.base-registry-username=${{ github.actor }}`
  - `-Dquarkus.jib.base-registry-password=${{ secrets.GITHUB_TOKEN }}`
- Finally a file listing overview of the runner workspace is printed to the Actions workflow log.

[checkout]: https://github.com/marketplace/actions/checkout
[quarkus]: https://quarkus.io/
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[sed]: https://manpages.ubuntu.com/manpages/jammy/man1/sed.1.html
[containerregistry]: https://docs.github.com/enterprise-server@latest/packages/working-with-a-github-packages-registry/working-with-the-container-registry
[dockerlogin]: https://github.com/marketplace/actions/docker-login
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions
