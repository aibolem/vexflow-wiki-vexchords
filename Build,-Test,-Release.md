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

Build all libraries (production, debug, and tests):

    grunt

Clean the `build/` and `reference/` folders::

    grunt clean

# Test

Run tests on the command line:

    grunt test

To run tests in the browser, open `tests/flow.html` in a new browser tab. This will load the CJS version of VexFlow, from `vexflow/build/cjs/vexflow-debug-with-tests.js`. You can also try the following commands:

```sh
# Open the default browser to the flow.html test page.
grunt test:browser:cjs

# Open the default browser to `http://localhost:8080/tests/flow.html?esm=true`.
# A web server needs to be serving the `vexflow/` directory (e.g., `npx http-server`).
grunt test:browser:esm
```

Don't forget the [Visual Regression Tests](./Visual-Regression-Tests):

```sh
# reference images will be generated from the last known good build.
git checkout master

# builds vexflow and copies the build output into the reference/ directory.
grunt reference

git checkout <my-feature-branch>

# builds the feature branch and does a visual diff against the version in the reference/ directory.
npm run test:reference
```

## Watch mode

To watch source files and build automatically when a file changes:

```
grunt watch
```

# Publish with [release-it](https://www.npmjs.com/package/release-it)

We use [release-it](https://www.npmjs.com/package/release-it) to streamline the process of publishing to NPM and GitHub.

Run the following command on a single line:

```
GITHUB_TOKEN=__PERSONAL_ACCESS_TOKEN__   npm run release
```

To automate the release to GitHub, you need to have a personal access token with **repo** rights.

Generate one here: https://github.com/settings/tokens/new?scopes=repo&description=release-it

If you have 2FA enabled for NPM, you will need to provide a one time password to publish to NPM.

**release-it** will walk you though the steps:

```
$ GITHUB_TOKEN=__PERSONAL_ACCESS_TOKEN__   npm run release

🚀 Let's release vexflow (currently at 4.0.0)

? Select increment (next version): patch (4.0.1)
✔ echo add build/ folder
✔ git add -f build/
✔ git commit -m 'Add build/ for the release.'

? Publish vexflow to npm? Yes
? Please enter OTP for npm: __YOUR_ONE_TIME_PASSWORD__
? Commit (release vexflow version 4.0.1)? Yes
? Tag (4.0.1)? Yes
? Push? Yes
? Create a release on GitHub (Release 4.0.1)? Yes
✔ echo Successfully released vexflow v4.0.1 to 0xfe/vexflow.
✔ echo remove build/ folder
✔ git rm -r build/
✔ git commit -m 'Remove build/ after the release.'
🔗 https://www.npmjs.com/package/vexflow
🔗 https://github.com/0xfe/vexflow/releases/tag/4.0.1
🏁 Done (in 38s.)
```

## Pre-release [ alpha | beta | rc ]

`Gruntfile.js` defines a `release` task that accepts pre-release tags as arguments:

```
GITHUB_TOKEN=XYZ grunt release
GITHUB_TOKEN=XYZ grunt release:alpha
GITHUB_TOKEN=XYZ grunt release:beta
GITHUB_TOKEN=XYZ grunt release:rc
```

Adding a `dry-run` argument will walk you through the steps without actually publishing anything.

```
GITHUB_TOKEN=XYZ grunt release:dry-run
GITHUB_TOKEN=XYZ grunt release:dry-run:alpha
GITHUB_TOKEN=XYZ grunt release:dry-run:beta
GITHUB_TOKEN=XYZ grunt release:dry-run:rc
```

You can run a pre-release multiple times, and it will increment the pre-release number.

```
4.1.0-alpha.1 => 4.1.0-alpha.2
```

https://www.npmjs.com/package/vexflow?activeTab=versions

## Publish Manually to npm and GitHub

The `npm version` command increments the version number in `package.json` and commits a new git tag to the repository:

```sh
# Usage: npm version [<new_version> | major | minor | patch | prerelease --preid=<alpha | beta | rc>]

# Show the current version.
npm version

# Bump the version. Add a git tag. Commit to the local git repo with a message.
# patch revision: X.Y.0 => X.Y.1
npm version patch --git-tag-version=false
# minor revision: X.1.Z => X.2.0
npm version minor --git-tag-version=false
# major revision: 4.Y.Z => 5.0.0
npm version major --git-tag-version=false

# Pre-release: alpha | beta | rc
npm version prerelease --preid=alpha --git-tag-version=false
npm version prerelease --preid=beta  --git-tag-version=false
npm version prerelease --preid=rc    --git-tag-version=false

```

Build VexFlow for production, and add the `build/` directory to the repository, and commit and tag this release.

```
grunt
git add -f build/
git commit -m "Release version: $(node -p "require('./package.json').version")"
git tag $(node -p "require('./package.json').version")
```

### Publish to npm

```sh
npm login

# Publish to 'latest' so that 'npm install vexflow' will get this version.
npm publish

# Publish with a pre-release tag. Example: npm install vexflow@beta will download the version published with --tag beta.
npm publish --tag rc
npm publish --tag beta
npm publish --tag alpha
```

### Release to GitHub

Push the git tag of the build we are releasing. For example, if the tag is `4.0.0`:

```sh
git push origin 4.0.0
```

Create a GitHub release from the tag we just pushed.

If you have the [GitHub CLI](https://cli.github.com/) installed:

```sh
# Create a release from the specified tag.
gh release create 4.0.0 --title "Release 4.0.0"

# Create a release from the version number in the package.json.
VEX_VER=$(node -p "require('./package.json').version") && gh release create $VEX_VER --title "Release $VEX_VER"
```

If you don't have the GitHub CLI, you can create a release from the web:

https://github.com/0xfe/vexflow/releases/new

![Choose Tag](images/github-release-choose-tag.png)

If something went wrong and you need to remove a version tag:

```sh
# Remove local tag
git tag --delete 4.0.0

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
