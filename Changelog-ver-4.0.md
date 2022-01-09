# 4.0.0

4.0.0 is the first major release of VexFlow since version 3.0.9 in April 2020.

This document details the major changes, and includes links to PRs or issues where appropriate.

The list of [breaking changes](#breaking-changes) is at the bottom of this page.

## TypeScript

VexFlow has been converted to TypeScript!

## ES Modules + Common JS

VexFlow now provides an ESM build, in addition to the traditional CommonJS library that works with `require()`.

## Breaking Changes

### Gruntfile and package.json scripts
Many of the package.json scripts have been moved into Gruntfile.js. See the top of Gruntfile.js for a list of the different commands you can invoke while building & testing VexFlow. If you previously used commands like `npm run xxxx`, you can look for the equivalent command in the Gruntfile.js (in most cases, `npm run xxxx` changed to `grunt xxxx`).

### More
[Add Detail Here]

### More
[Add Detail Here]
