_Note that these instructions are for the new pure-JS toolchain in the `browserify` branch._

## Quick Build

If you have NodeJS and `npm` installed:

   $ git clone _this repository_
   $ npm install
   $ npm start
   $ npm test

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

# Using the old Ruby toolchain

## Prerequisites

VexFlow builds require a Ruby installation and are built with the [Rake](http://rake.rubyforge.org/) build tool.

* Rake
* Uglifier
* Git
* [JSHint](http://jshint.com) - For code linting.
* [Docco](http://jashkenas.github.io/docco/) - For generating documentation.

To get all the Ruby dependencies, you can use Bundler:

    $ gem install bundler
    $ bundle install

JSHint and Docco can be installed with NPM.

    $ npm install jshint
    $ npm install docco

## Building

Build with:

    $ rake

Clean with:

    $ rake clean

If you have [JSHint](http://jshint.com) installed, you can check your code for
common errors with the following command. Note that this step is mandatory if
you want to commit your changes into the official VexFlow repository.

    $ rake lint

To regenerate documentation from code, you need [Docco](http://jashkenas.github.io/docco/), which lets you embed Markdown syntax in comments. Fixing up comments is currently a work-in-progress, and any new code must conform to the commenting style (see `src/accidental.js` for an example). Use the following command to generate documentation.

    $ rake docs