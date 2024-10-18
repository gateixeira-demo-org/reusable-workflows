# JUnit reusable workflow details

> [JUnit][junit] is a unit testing framework for the Java programming language.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step the repository code is checked out to the runner using the [Checkout][checkout] action.
- Java is installed using the [Setup Java JDK][setupjava] action. The `github/setup-java@v4` action is used to set up a Java JDK environment. [Version][version] and [distribution][distribution] can be manually configured, other available parameters can be found in the setup-java repo.
- If the workflow is triggered by release, the tag belonging to the release is used to set the version of the project inside the `pom.xml` file using the [revision][revision] flag.
- The [`maven-surefire-plugin`][mavensurefire] is used to run the unit tests.
- A result report is generated and used as a gatekeeper for the workflow using the [Test Reporter][testreporter] Action.
  This test report is published in the Action job summary view.
- Finally a file listing overview of the runner workspace is printed to the Actions workflow log.

[checkout]: https://github.com/marketplace/actions/checkout
[mavensurefire]: https://maven.apache.org/surefire/maven-surefire-plugin/
[junit]: https://junit.org/
[setupjava]: https://github.com/marketplace/actions/setup-java-jdk
[testreporter]: https://github.com/marketplace/actions/test-reporter
[revision]: https://maven.apache.org/maven-ci-friendly.html
[distribution]: https://github.com/actions/setup-java#supported-distributions
[version]: https://github.com/actions/setup-java#supported-version-syntax
[workflowsyntax]: https://docs.github.com/enterprise-server@latest/actions/using-workflows/workflow-syntax-for-github-actions