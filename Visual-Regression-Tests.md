## About

VexFlow comes with a visual regression test system. All VexFlow QUnit tests (the ones in `tests/`) that generate images are automatically included in these regression tests.

The goal of this system is to detect regressions in the rendered output without having to rely on human eyeballs, especially given the huge number of tests that exist today. It does this by calculating a [perceptual hash](https://en.wikipedia.org/wiki/Perceptual_hashing) (PHASH) of each test image and comparing it with the hash of a good known _blessed_ image. The larger the arithmetic distance between the hashes, the more different are the two images.

The system also generates a _diff image_, which is an overlay of the two images, with the differences highlighted, to ease debugging.

## Crude Example
Below you can see an example of a blessed image, a current image, and the visual difference (value 27.649.)

<image src="https://i.imgur.com/Oms9i2b.png" width=200>
![Current Image](https://i.imgur.com/dYMEohn.png)
![Difference](https://i.imgur.com/ypz5det.png)

## Prerequisites

The test system relies on the open-source libraries, [RSVG](https://github.com/GNOME/librsvg) and [ImageMagick](http://www.imagemagick.org/).

Installing on OS X, with HomeBrew: `$ brew install librsvg imagemagick`

Installing on Ubuntu Linux: `$ apt-get install librsvg2-dev librsvg2-bin imagemagick`

## How to Test
After you install the dependencies, you can start the test by running the following commands:

```
$ npm run generate
$ npm run diff
```

This will store the images of the failed tests (i.e., where there are visible differences) in `build/images/diff`. Visually inspect these images (including the diff image), and if you're happy with the output you can simply submit your changes. Be sure to include the before, after, and diff images in your pull request.

## How it Works

The `npm run generate` command generates images from the current code-base. Files are named by their QUnit module and test name. The last-good-known-images are generated from the last released binaries and stored in `build/images/blessed`. The images from the current code are stored in `build/images/current`.

The `npm run diff` command calculates the PHASH values to detect images that have changed significantly. These images are stored in `build/images/diff`. There also the files `results.txt` and `warnings.txt` with the complete results.

The current version of `visual_regression.sh` does the following:

* For all SVG files in `build/images/blessed`:
 * Find the relevant file in `build/images/current`.
 * Convert both to PNG.
 * Calculate the PHASH (perceptual hash) of each and report the difference.
 * Store the file name and difference value in `build/images/diff/results.txt`
 * If the difference is greater than a predefined threshold (0.01), copy the current, blessed, and a special "diff-image" to `build/images/diff`. The diff-image visually highlights the differences.
* Sort `build/images/diff/results.txt` by PHASH difference.

You can examine the `results.txt` file and looks for images fall below the threshold. If you're seeing too many false positives, you can also adjust the threshold in `tools/visual_regression.sh`.