## Changelog

Versioning complies with [semantic versioning (semver)](http://semver.org/).

<!-- NOTE: An entry template is automatically added each time `make version` is called. Fill in changes afterwards. -->

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

