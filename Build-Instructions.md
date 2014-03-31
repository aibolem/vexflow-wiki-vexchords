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

## Build Instructions

Build with:

    $ rake

Clean with:

    $ rake clean

If you have [JSHint](http://jshint.com) installed, you can check your code for
common errors with the following command. Note that this step is mandatory if
you want to commit your changes into the official VexFlow repository.

    $ rake lint

To regenerate documentation from code, you need [Docco](http://jashkenas.github.io/docco/), which lets you embed Markdown syntax into code. Fixing up comments is currently a work-in-progress, and any new code must conform to the commenting style (see `src/accidental.js` for an example). Use the following command to generate documentation.

    $ rake docs