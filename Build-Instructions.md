To setup the build environment, first install NodeJS and `npm`. Then, from the `vexflow/` directory (this repo), run:

    $ git clone _this repository_
    $ npm install
    $ npm install -g grunt-cli

Note that you can also install `grunt-cli` locally (without the -g flag). If you do so, you'll need to fully qualify the path in the commands below: `./node_modules/.bin/grunt`.

## Building

Build with:

    $ grunt

Clean with:

    $ grunt clean

Run tests on command line:

    $ grunt test

To run tests in the browser, open `tests/flow.html` in a new browser tab. Don't forget the [Visual Regression Tests](https://github.com/0xfe/vexflow/wiki/Visual-Regression-Tests).

To publish a new version of VexFlow to the NPM repositories:

    $ npm login
    $ grunt publish

This bumps the version number in `package.json`, publishes the new NPM package, and submits the new binaries to the git repo.

## Upgrading Dependencies

First install the [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) package, which automates the process of finding and upgrading the versions in `package.json`.

    $ npm cache clean
    $ npm install -g npm-check-updates

Dry run. This checks for new versions, but does not modify any files.

    $ npm-check-updates

If the versions look sane, you can either update everything in one shot, or provide a package name to update incrementally. The `-u` flag updates `package.json`.

    $ npm-check-updates -u [package name]
    $ npm install

Test, debug, fix, commit, iterate. Then send a PR!