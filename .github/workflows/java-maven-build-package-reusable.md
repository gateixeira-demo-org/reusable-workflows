# Build package reusable workflow details

> Build Java package with Maven.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v4` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- If the workflow is triggered by release, the tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [revision][revision] flag.
- The Java package is built using the [maven][maven].
- Finally a file listing overview of the runner workspace is printed to the Actions workflow log.

[superlinter]: https://github.com/marketplace/actions/super-linter
[checkout]: https://github.com/marketplace/actions/checkout
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[revision]: https://maven.apache.org/maven-ci-friendly.html
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/en/enterprise-cloud@latest/actions/writing-workflows
[maven]: https://maven.apache.org/
