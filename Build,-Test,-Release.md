# Prerequisites

Make sure you have installed [Node.js](https://nodejs.org/) 16.x or greater and [npm](https://docs.npmjs.com/cli/v7/configuring-npm/install#using-a-node-version-manager-to-install-nodejs-and-npm).

We use the `grunt` task runner, so install [grunt-cli](https://www.npmjs.com/package/grunt-cli) globally.

    npm install -g grunt-cli

If you do not install **grunt-cli** globally, you'll need to use the full path to the local `grunt` command:

    ./node_modules/.bin/grunt

# Download the Source and Install Dependencies

```
git clone git@github.com:0xfe/vexflow.git
cd vexflow
npm install
```

# Build

Build everything, including libraries for production use, debugging, and unit tests:

    grunt

Clean with:

    grunt clean

# Test

Run tests on command line:

    grunt test

To run tests in the browser, open `tests/flow.html` in a new browser tab.

Don't forget the [[Visual Regression Tests]].

## Watch mode

To watch source files for changes and build automatically, use the following commands:

```sh
# Watch src/ tree and build unminimized bundle
grunt webpack:watch

# Watch test/ tree and rebuild test bundle
grunt watch
```

## Publishing Manually

-   Bump version in `package.json`
-   `git commit`.
-   xxxxxxx
-   Push new git tag.
-   Log into NPM: `npm login`
-   Publish: `npm publish [--tag beta]`

### Push a version tag to GitHub

    git push origin 4.0.0

### Remove version tag from local repo and GitHub

```sh
# Remove local tag
git tag -d 4.0.0

# Remove remote tag
git push --delete origin 4.0.0
```

# Upgrade Dependencies

Install [npm-check-updates](https://www.npmjs.com/package/npm-check-updates), which automates the process of finding and upgrading the versions in `package.json`.

    npm install -g npm-check-updates

Dry run: Invoke the command with no arguments to check for new versions. This does not modify any files.

    npm-check-updates

If the versions look sane, you can either update everything in one shot, or provide a package name to update incrementally. The `-u` flag updates `package.json`.

    npm-check-updates -u [package name]
    npm install

Build, test, debug, fix, iterate. If everything works and there are no visual diffs, commit your changes and submit a PR!
