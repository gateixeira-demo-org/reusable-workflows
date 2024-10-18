> [npm][npm] is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js.

:bulb: Workflow files are constructed following the documented [GitHub Actions workflow syntax][workflowsyntax].

## Workflow details

- As a first step, the repository code is checked out to the runner using the [Checkout][checkout] action.
- Node.js is installed using the [Setup Node.js][setupnode] action. The `actions/setup-node@v4` action is used to set up a Node.js environment. [Version][nodeversion] can be manually configured, other available parameters can be found in the setup-node repo.
- If the workflow is triggered by a release event, the package version is set using the `npm version` command.
- Dependencies are installed using the `npm install` command.
- The `npm run build` command is used to build the npm package.

[checkout]: https://github.com/marketplace/actions/checkout
[npm]: https://www.npmjs.com/
[setupnode]: https://github.com/marketplace/actions/setup-node-js-environment
[nodeversion]: https://github.com/actions/setup-node#usage
[workflowsyntax]: https://docs.github.com/en/enterprise-cloud@latest/actions/writing-workflows