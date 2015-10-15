## About

VexFlow comes with a visual regression test system. All VexFlow QUnit tests (the ones in `tests/`) that generate images are automatically included in these regression tests. Blessed images are stored in `tests/blessed` as SVG files.

The goal of this system is to detect regressions in the rendered output without having to rely on human eyeballs, especially given the huge number of tests that exist today. It does this by calculating a [perceptual hash](https://en.wikipedia.org/wiki/Perceptual_hashing) (PHASH) of each test image and comparing it with the hash of a good known _blessed_ image. The larger the arithmetic distance between the hashes, the more different are the two images.

The system also generates a _diff image_, which is an overlay of the two images, with the differences highlighted, to ease debugging.

## Prerequisites

The test system relies on the open-source libraries, [RSVG](https://github.com/GNOME/librsvg) and [ImageMagick](http://www.imagemagick.org/).

Installing on OS X, with HomeBrew: `$ brew install librsvg imagemagick`

Installing on Ubuntu Linux: `$ apt-get install librsvg2-dev librsvg2-bin imagemagick`

## How to Test

After installing the dependencies, run `tools/generate_svg_images.js` to generate images from the current code-base. Files are named by their QUnit module and test name.

To start the test, run `tools/visual_regression.sh`, which will call out tests for which the images have changed significantly.

Visually inspect the images (including the diff image), and if you're happy with the changes, you can bless the SVG by copying it from `build/images` to `tests/blessed`.

Submit your changes, along with the blessed SVG. Be sure to include the before, after, and diff images in your pull request.

## How it Works

The current version of `visual_regression.sh` does the following:

* For all SVG files in `tests/blessed`:
 * Find the relevant file in `build/images`.
 * Convert both to PNG.
 * Calculate the PHASH (perceptual hash) of each and report the difference.
 * Store the file name and difference value in `build/images/diff/results.txt`
 * If the difference is greater than a predefined threshold (1.0), store a special "diff-image" PNG in `build/images/diff`, which visually highlights the differences.
 * Open all three files (blessed, current, diff) using your system image viewer for inspection.
* Sort `build/images/diff/results.txt` by PHASH difference.

You can examine the `results.txt` file and looks for images fall below the threshold. If you're seeing too many false positives, you can also adjust the threshold in `visual_regression.sh`.