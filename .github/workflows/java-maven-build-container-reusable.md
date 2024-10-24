> Build container with Maven and Docker.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- The repository code is checked out to the runner using the [Checkout action][checkout].
- Java is installed using the Setup Java JDK action. The [github/setup-java@v4][setupjava] action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- The Artifact Name is retrieved from `<artifactId>` in the pom.xml file using [SED][sed] to be used as part of the docker tag.
- The Git short hash is set to compose the tag.
- The image prefix is set to include the container registry URL and the repository owner.
- If the workflow is triggered by a release, the tag belonging to the release is used to set the version of the project inside the pom.xml file using the revision flag via a Docker ARG variable.
- The container image name is formulated as `<registry-url>/<repository-owner>/<artifact-name>:<revision>_<git-short-sha>`. If the workflow is not triggered by a release, we remove revision from the tag: `<registry-url>/<repository-owner>/<artifact-name>:<git-short-sha>`.
- The container is built using docker build directly.
- Docker Buildx is set up for more comprehensive build options using the [docker/setup-buildx-action@v3][dockerbuildx].
- The container registry login is handled using the [docker/login-action@v3][dockerlogin] action.
- The container is built and pushed if there is a release to the registry using the [docker/build-push-action@v6][dockerbuildpush] action.
- Different cache strategies are in place for the build process, using GitHub Actions cache.

[checkout]: https://github.com/marketplace/actions/checkout
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[sed]: https://manpages.ubuntu.com/manpages/jammy/man1/sed.1.html
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions
[docker]: https://docs.docker.com/build/
[dockerlogin]: https://github.com/docker/login-action
[dockerbuildpush]: https://github.com/docker/build-push-action
[dockerbuildx]: https://github.com/docker/setup-buildx-action