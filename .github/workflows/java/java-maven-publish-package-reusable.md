# Publish package reusable workflow details

> Publish Java package to GitHub Packages using Maven with [Quarkus framework][quarkus].

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v3` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- The tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [SED][sed] command.
- The [GitHub Maven package registry][mavenregistry] URL is constructed by available repository context and set as an environment variable using the [SED][sed] command.
- The Java package is built and published using the Maven wrapper part of the Quarkus framework. The GitHub Maven package registry URL is set as a parameter.
- Finally a file listing overview of the runner workspace is printed to the Actions workflow log.

[checkout]: https://github.com/marketplace/actions/checkout
[quarkus]: https://quarkus.io/
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[sed]: https://manpages.ubuntu.com/manpages/jammy/man1/sed.1.html
[mavenregistry]: https://docs.github.com/enterprise-server@latest/packages/working-with-a-github-packages-registry/working-with-the-apache-maven-registry
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions
