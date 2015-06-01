[![npm version](https://badge.fury.io/js/rreadlink.svg)](http://badge.fury.io/js/rreadlink)

# rreadlink

A **multi-platform Unix CLI** that **prints a symlink's _complete chain_ of targets** using **_absolute_ paths**.

The primary purpose of `rreadlink` (*r*ecursive *readlink*) is to _follow a given symlink to its ultimate target_, printing _all intermediate symlinks_ along the way.  
All paths are printed as _absolute_ paths, with the ultimate target printed in _canonical_ form.

This is hepful on Linux platforms, for instance, where some utilities are installed as symlinks that point to _other_ symlinks before resolving
to the ultimate target, making it difficult to understand what is ultimately invoked; e.g., on some Linux distros `/usr/bin/nawk` links to `/etc/alternatives/nawk`, which in turn links to the actual target, `/usr/bin/gawk`.  
Note that the native GNU `readline` can either only give you the _next_ target (not the ultimate one), or, with `-f` or `-e` or `-m`, _only_ the _ultimate_ target (not intermediate ones).

Loosely speaking, `rreadlink` provides the functionality of GNU `readline -e` while also including _intermediate_ targets.
`rreadlink` has the added advantage of being multi-platform (see [Supported Platforms](#supported-platforms) below).

Alternatively, given a _non_-symlink, `rreadlink` prints the argument's canonical path (i.e., any _directory_ components that are symlinks are resolved to their ultimate targets).

See the [Usage](#usage) chapter for details.

<sup>**See also**: [`typex`](https://github.com/mklement0/typex) provides information about _executables in the path_ (among other things) and has `rreadlink`'s behavior built in to show what file is ultimately invoked.</sup>

## Supported Platforms

Any Unix-like platform with POSIX-compatible utilities, with `bash` installed; for instance, Linux and OS X.

## Quick Examples

```shell
# Print the symlink chain for executable /usr/bin/nawk (e.g., on Ubuntu):
$ rreadlink /usr/bin/nawk
/usr/bin/nawk@ -> /etc/alternatives/nawk@ -> /usr/bin/gawk

# Ditto, but printing one path per line, without the symlink sigil (@):
# (This format is the default when not outputting to a terminal.)
$ rreadlink -1 /usr/bin/nawk
/usr/bin/nawk
/etc/alternatives/nawk
/usr/bin/gawk

# Canonicalize the path of a non-symlink:
# (Assume that /var links to /private/var and that log is a regular file.)
$ rreadlink /var/log
/private/var/log

```

## Installation

With [node.js](http://nodejs.org/) installed, install via the [npm registry](https://www.npmjs.com/) (you may have to prepend `sudo`):

	npm install rreadlink -g

## Usage

<!-- DO NOT EDIT THE FENCED CODE BLOCK and RETAIN THIS COMMENT: The fenced code block below is updated by `make update-readme/release` with CLI usage information. -->

```
$ rreadlink --help


SYNOPSIS
  rreadlink [-s|-1] symLink
  rreadlink -e symLink

DESCRIPTION
  Recursive readlink: prints the CHAIN OF SYMLINKS
  from the input file to its ultimate target, using ABSOLUTE PATHS.

  -s
    Short output format - a single line is output with ' -> ' between paths,
    with symlinks marked with a terminal '@' (similar to  `ls -lF`).
    This is the default output format when printing to a terminal.

  -1 
    (The number one.) One-line-per-path output format.
    Prints each output path on its own line, without the terminal '@'.
    This is the default output format when not printing to a terminal.

  -e
    Prints only the *ultimate* target's absolute path.
    Same as GNU readlink's -e (--canonicalize-existing) option.
  
  If the input file is indeed a symlink, you'll get at least 2
  output paths (unless -e is specified): the input symlink and its
  target; if there are intermediate symlinks, you'll get more.

  While each file is output by its absolute path, it is only
  the *ultimate* target whose path will be *canonical*.

  CAVEAT: *Circular* symlinks are NOT detected and will result in
  an infinite loop.

  If any of the files in the chain do not exist, processing
  stops, an error message is output and exit code 1 is returned.

  If the input file is NOT a symlink, only *its* full path is
  printed in its *canonical* form. I.e., the file's directory
  path - if it happens to have symlink components - is resolved to
  its ultimate target.

  Thus, you can use
    rreadlink -e anyFile
  on any existing filesystem object, and you'll either get its own
  canonical path (if not a symlink) or its ultimate target's canonical
  path (if a symlink).

EXAMPLES
    # Prints the chain of symlinks for the `git` executable
    # in the $PATH.
  rreadlink $(which git)
    # Prints the canonicalized path of the given non-symlink.
    # (Example from OSX, where /var links to /private/var.)
  rreadlink /var/log  # -> '/private/var/log'
```

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'LICENSE.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

## License

Copyright (c) 2015 Michael Klement, released under the [MIT license](https://spdx.org/licenses/MIT#licenseText).

### Acknowledgements

This project gratefully depends on the following open-source components, according to the terms of their respective licenses.

[npm](https://www.npmjs.com/) dependencies below have optional suffixes denoting the type of dependency; the absence of a suffix denotes a required run-time dependency: `(D)` denotes a development-time-only dependency, `(O)` an optional dependency, and `(P)` a peer dependency.

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the dependencies from 'package.json'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

### npm dependencies

* [json (D)](https://github.com/trentm/json)
* [replace (D)](https://github.com/harthur/replace)
* [semver (D)](https://github.com/npm/node-semver#readme)
* [shall (D)](https://github.com/mklement0/shall)
* [urchin (D)](https://github.com/tlevine/urchin)

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'CHANGELOG.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

## Changelog

Versioning complies with [semantic versioning (semver)](http://semver.org/).

<!-- NOTE: An entry template is automatically added each time `make version` is called. Fill in changes afterwards. -->

* **v0.1.4** (2015-05-30):
  * [doc] [npm registry badge[(https://badge.fury.io) added.

* **v0.1.3** (2015-02-11):
  * Doc: Read-me improvements.

* **v0.1.2** (2015-02-11):
  * Doc: Read-me and CLI help improvements.

* **v0.1.1** (2015-02-11):
  * Dev: Tests improved.

* **v0.1.0** (2015-02-11):
  * Initial release.
