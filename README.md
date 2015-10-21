[![npm version](https://img.shields.io/npm/v/rreadlink.svg)](https://npmjs.com/package/rreadlink) [![license](https://img.shields.io/npm/l/rreadlink.svg)](https://github.com/mklement0/rreadlink/blob/master/LICENSE.md)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Contents**

- [rreadlink &mdash; introduction](#rreadlink-&mdash-introduction)
- [Examples](#examples)
- [Installation](#installation)
  - [Installation from the npm registry](#installation-from-the-npm-registry)
  - [Manual installation](#manual-installation)
- [Usage](#usage)
- [License](#license)
  - [Acknowledgements](#acknowledgements)
  - [npm dependencies](#npm-dependencies)
- [Changelog](#changelog)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# rreadlink &mdash; introduction

`rreadlink` is a **multi-platform Unix CLI** that **prints a symlink's _complete chain_ of targets** using **_absolute_ paths**; it can
also determine the canonical path of non-symlinks.

The primary purpose of `rreadlink` (*r*ecursive *readlink*) is to follow a given symlink to its ultimate target, printing _all intermediate symlinks_ along the way.  
All paths are printed as _absolute_ paths, with the ultimate target printed in _canonical_ form.

This is hepful on Linux platforms, for instance, where some utilities are installed as symlinks that point to _other_ symlinks before resolving
to the ultimate target, making it difficult to understand what is ultimately invoked;  
e.g., on some Linux distros `/usr/bin/nawk` links to `/etc/alternatives/nawk`, which in turn links to the actual target, `/usr/bin/gawk`.  
Note that the native GNU `readlink` utility can either only give you the _next_ target (not the ultimate one), or, with `-f` or `-e` or `-m`,
_only_ the _ultimate_ target (not intermediate ones).

Loosely speaking, `rreadlink` provides the functionality of GNU `readlink -e` while also including _intermediate_ targets.
`rreadlink` has the added advantage of being multi-platform (see [Installation](#installation) below).

Alternatively, given a _non_-symlink, `rreadlink` prints the argument's canonical path (i.e., any _directory_ components that are symlinks
are resolved to their ultimate targets).

Find examples below, concise [usage information](#usage) further below, or
read the [manual](doc/rreadlink.md).

<sup>**See also**: The [`typex`](https://github.com/mklement0/typex) utility
provides information about _executables in the path_ (among other things) and
has `rreadlink`'s behavior built in to show what file is ultimately invoked.</sup>

# Examples

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

# Installation

**Supported platforms**

**Unix-like platforms** with **POSIX-compatible utilities** and
[Bash](http://www.gnu.org/software/bash/), such as Linux and OS X.

## Installation from the npm registry

<sup>Note: Even if you don't use Node.js, its package manager, `npm`, works across platforms and is easy to install; try [`curl -L http://git.io/n-install | bash`](https://github.com/mklement0/n-install)</sup>

With [Node.js](http://nodejs.org/) or [io.js](https://iojs.org/) installed, install [the package](https://www.npmjs.com/package/rreadlink) as follows:

    [sudo] npm install rreadlink -g

**Note**:

* Whether you need `sudo` depends on how you installed Node.js / io.js and whether you've [changed permissions later](https://docs.npmjs.com/getting-started/fixing-npm-permissions); if you get an `EACCES` error, try again with `sudo`.
* The `-g` ensures [_global_ installation](https://docs.npmjs.com/getting-started/installing-npm-packages-globally) and is needed to put `rreadlink` in your system's `$PATH`.

## Manual installation

* Download [the CLI](https://raw.githubusercontent.com/mklement0/rreadlink/stable/bin/rreadlink) as `rreadlink`.
* Make it executable with `chmod +x rreadlink`.
* Move it or symlink it to a folder in your `$PATH`, such as `/usr/local/bin` (OSX) or `/usr/bin` (Linux).


# Usage

Find concise usage information below; for complete documentation, read the [manual online](doc/rreadlink.md) or,
once installed, run `rreadlink nws` (`rreadlink --man` if installed manually).

<!-- DO NOT EDIT THE FENCED CODE BLOCK and RETAIN THIS COMMENT: The fenced code block below is updated by `make update-readme/release` with CLI usage information. -->

```nohighlight
$ rreadlink --help


Recursively resolves symlinks by printing the chain of targets using absolute  
paths or prints the canonical path of a symlink's ultimate target or of a  
non-symlink.

    rreadlink [-s|-1] symLink
    rreadlink -e symLink

    -s     single-line output format using ' -> ' between paths and
           @ to mark symlinks (default when printing to terminal)
    -1     one-line-per-path output format, without the @ marker (default
           when NOT printing to a terminal)
    -e     print only the symlink's ultimate target, in canonical form

Standard options: --help, --man, --version, --home
```

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'LICENSE.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

# License

Copyright (c) 2015 Michael Klement <mklement0@gmail.com> (http://same2u.net),
released under the [MIT license](https://spdx.org/licenses/MIT#licenseText).

## Acknowledgements

This project gratefully depends on the following open-source components, according to the terms of their respective licenses.

[npm](https://www.npmjs.com/) dependencies below have optional suffixes denoting the type of dependency; the absence of a suffix denotes a required run-time dependency: `(D)` denotes a development-time-only dependency, `(O)` an optional dependency, and `(P)` a peer dependency.

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the dependencies from 'package.json'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

## npm dependencies

* [doctoc (D)](https://github.com/thlorenz/doctoc)
* [json (D)](https://github.com/trentm/json)
* [marked-man (D)](https://github.com/kapouer/marked-man#readme)
* [replace (D)](https://github.com/harthur/replace)
* [semver (D)](https://github.com/npm/node-semver#readme)
* [shall (D)](https://github.com/mklement0/shall)
* [urchin (D)](https://github.com/tlevine/urchin)

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'CHANGELOG.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

# Changelog

Versioning complies with [semantic versioning (semver)](http://semver.org/).

<!-- NOTE: An entry template is automatically added each time `make version` is called. Fill in changes afterwards. -->

* **[v0.2.1](https://github.com/mklement0/rreadlink/compare/v0.2.0...v0.2.1)** (2015-10-21):
  * [dev] Improved robustness of interal `rreadlinkchain()` function.

* **[v0.2.0](https://github.com/mklement0/rreadlink/compare/v0.1.6...v0.2.0)** (2015-09-18):
  * [potentially breaking change] `rreadlink` now also accepts options placed
      _after_ operands on the command line (except after `--`).
  * [doc] `rreadlink` now has a man page (if manually installed, 
      use `rreadlink --man`); `rreadlink -h` now just prints concise usage
      information.
  * [doc] `README.md` cleaned up and extended.
  * [dev] Removed post-install command that verifies presence of Bash, because
    `npm` _prints_ the command during installation, which can be confusing.

* **[v0.1.6](https://github.com/mklement0/rreadlink/compare/v0.1.5...v0.1.6)** (2015-09-15):
  * [dev] Makefile improvements; various other behind-the-scenes tweaks.

* **[v0.1.5](https://github.com/mklement0/rreadlink/compare/v0.1.4...v0.1.5)** (2015-06-26):
  * [doc] Read-me: npm badge changed to shields.io; license badge added; typo fixed.
  * [dev] To-do added; Makefile updated.

* **v0.1.4** (2015-05-30):
  * [doc] [npm registry badge](https://badge.fury.io) added.

* **v0.1.3** (2015-02-11):
  * Doc: Read-me improvements.

* **v0.1.2** (2015-02-11):
  * Doc: Read-me and CLI help improvements.

* **v0.1.1** (2015-02-11):
  * Dev: Tests improved.

* **v0.1.0** (2015-02-11):
  * Initial release.
