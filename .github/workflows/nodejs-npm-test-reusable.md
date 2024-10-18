> [npm][npm] is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step, the repository code is checked out to the runner using the [Checkout][checkout] action.
- Node.js is installed using the [Setup Node.js][setupnode] action. The `actions/setup-node@v4` action is used to set up a Node.js environment. [Version][nodeversion] can be manually configured, other available parameters can be found in the setup-node repo.
- Dependencies are installed using the `npm install` command.
- The `npm test` command is used to run the unit tests.
- A result report is generated and used as a gatekeeper for the workflow using the [Test Reporter][testreporter] Action. This test report is published in the Action job summary view.

[checkout]: https://github.com/marketplace/actions/checkout
[npm]: https://www.npmjs.com/
[setupnode]: https://github.com/marketplace/actions/setup-node-js-environment
[testreporter]: https://github.com/marketplace/actions/test-reporter
[nodeversion]: https://github.com/actions/setup-node#usage
[workflowsyntax]: https://docs.github.com/en/enterprise-cloud@latest/actions/writing-workflows