# image-optim [![Build Status](https://travis-ci.org/eGavr/image-optim.svg)](https://travis-ci.org/eGavr/image-optim) [![Dependency Status](https://david-dm.org/eGavr/image-optim.svg)](https://david-dm.org/eGavr/image-optim) [![devDependency Status](https://david-dm.org/eGavr/image-optim/dev-status.svg)](https://david-dm.org/eGavr/image-optim#info=devDependencies)

Node.js wrapper for some images compression algorithms: [PNGOUT](http://www.advsys.net/ken/util/pngout.htm), [Zopfli](http://googledevelopers.blogspot.co.uk/2013/02/compress-data-more-densely-with-zopfli.html), [Pngcrush](http://pmt.sourceforge.net/pngcrush/), [AdvPng](http://advancemame.sourceforge.net/doc-advpng.html) and [OptiPNG](http://optipng.sourceforge.net/).

## Install

```bash
$ npm install image-optim
```

## Usage

### API

```js
var imageOptim = require('image-optim');
```

#### imageOptim.optim

Optimizes the given files.

**@param** *{Array}* - a list of paths to files to optimize<br>
**@returns** *{Promise * Array}* - the information about optimized files:<br>

```js
[{ name: 'file.ext', savedBytes: 12345, exitCode: 0 }]
```

#### imageOptim.lint

Checks whether the given files can be optimized further.

**@param** *{Array}* - a list of paths to files to check<br>
**@param** *{Object}* - options:<br>

  * **tolerance** *{Number}* - sets the _measurement error_ during the check. If the difference in sizes between the raw file and the compressed file is less than or equal to the specified _tolerance_, **image-optim** will consider that the raw file can not be optimized further (default: `0`)

**@returns** *{Promise * Array}* - the information about linted files:<br>

```js
[{ name: 'file.ext', isOptimized: false, exitCode: 0 }]
```

#### imageOptim.SUCCESS

If the file was processed without errors its exit code will be equal to `0`.

#### imageOptim.CANT_COMPRESS

If the file can not be compressed its exit code will be equal to `1`.

#### imageOptim.DOESNT_EXIST

If the file does not exist its exit code will be equal to `2`.

### CLI

```bash
$ image-optim --help
Node.js wrapper for some images compression algorithms

Usage:
  image-optim [OPTIONS] [ARGS]

Options:
  -h, --help : Help
  -v, --version : Shows the version number
  -l, --lint : Lint mode
  -t TOLERANCE, --tolerance=TOLERANCE : Tolerance (default: 0)

Arguments:
  FILES : Paths to files (required)
```
