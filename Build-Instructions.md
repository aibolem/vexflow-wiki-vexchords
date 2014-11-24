## Quick Build

If you have NodeJS and `npm` installed:

    $ git clone _this repository_
    $ npm install
    $ npm start
    $ npm test

The above steps downloads, builds, and executes the tests for VexFlow.

## The Long Way

To setup the build environments, first install NodeJS and `npm`. Then, from the `vexflow/` directory (this repo), run:

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

To run tests in the browser, open `tests/flow.html` in a new browser tab.

To publish a new version of VexFlow to the NPM repositories:

    $ npm login
    $ grunt publish

This bumps the version number in `package.json`, publishes the new NPM package, and submits the new binaries to the git repo.