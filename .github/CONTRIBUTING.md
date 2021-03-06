# Contributing To Kamailio #

*First, thank you for taking the time to contribute to Kamailio project!*

The following is a set of guidelines for contributing to Kamailio sources and
documentation. Kamailio source tree is hosted in the [Kamailio Organization](https://github.com/kamailio) on GitHub.

These are intended to be more like guidelines to keep everything consistent and
coherent, not very strict rules. Use your best judgment and feel free to propose
changes to this document in a pull request.

### Table Of Contents ###

  * [Overview](#overview)
  * [Contributing Code Or Content](#contributing-code-or-content)
    * [Basic Rules](#basic-rules)
    * [Commit Message Format](#commit-message-format)
      * [Examples Of Commit Messages](#examples-of-commit-messages)
      * [See Also](#see-also)
  * [Reporting Issues](#reporting-issues)
  * [License](#license)
    * [License Of New Code Contributions](#license-of-new-code-contributions)
  * [Further Assistance](#further-assistance)

## Overview ##

Kamailio is a community managed project, with developers world wide. Any
contribution to code or documentation is very welcome and appreciated.

In order to be easily able to track the changes and have a coherent ChangLog
and commit history, there are several *rules* required for each contribution.

## Contributing Code Or Content ##

### Basic Rules ###

  * github pull requests are the favourited mechanism to submit contributions
  (patches)
  * make a pull request against **master branch**
    * commit can be later backported to stable branch(es)
  * make a pull request for each new feature
    * e.g., if you add a feature to usrloc module and an unrelated feature
    to auth module, then make two pull requests
  * it is ok (and sometime recommended) to have more than one commit per pull request
  * make a commit for each affected component. A component is considered to be:
    * the core
    * an internal library (code inside subfolder lib/)
    * a module (code inside subfolder modules/)
    * a tool (code inside subfolder utils/)
    * an example or main configs (files inside subfolders etc/ or examples/)
  * commit messages **has to be formatted** as specified in the next section
  * commit message must describe the changes done by the patch
    * other details (e.g., how to reproduce, backtrace, sip packets, ...) belong
    to content (comments) of the pull request
  * avoid emoticons and non-technical statements in commit messages
    * e.g., if it was a feature request by John Smith, don't mention that in
    commit message, especially don't write it owns you now a beer
  * credits can be given within commit message as a short statement, mentioning
  the name of the person or entity
    * for commits introducing a new module, credits must not be included in the
    commit message, being expected that the respective entity will own the
    copyright and it is reflected in the README or copyright header of each file
  * when the case, make references to the item on bug tracker, using GH #XYZ
  -- replace XYZ with issue number id
    * e.g.,: - issue reported by John Smith, GH #123
  * changes to **README** file of modules **must** not be done directly in that
  file. Instead, edit the xml files located in **modules/modname/doc/** folder
    * to regenerate the README, run **make modules-readme modules=modules/modname**
    * docbook utils and xsl packages are needed for the above command to work
    * it is ok to modify only the xml doc file, the readme can be regenerated by
    another developer who has the required tools installed
    * if it is a change to README that needs to be backported, make separate
    commits to xml doc file and README. The changes to README files are very
    likely to rise merge conflicts. With separate commit, that won't be
    backported, only the commit to xml doc file, then README will be manually
    regenerated in the corresponding branch.
  * code **should** be formatted with **clang-format** or to match the style of
  the component that the commit applies to. The `.clang-format` file is part of
  Kamailio source code tree, in the root folder.


### Commit Message Format ###

Please create the commit messages following the GIT convention:

  * start with one short line, preferably less then 50 chars summarizing the
  changes (this is referred later as "first line of the commit message")
  * then one empty line
  * then a more detailed description

Think of the first line as of an email "Subject" line. In fact it will be used
as "Subject" in the generated commit emails and it will also be used when
generating the Changelog (e.g. git log --pretty=oneline).

Please start always with the prefix of the component (subsystem) that is modified by the commit, for example:
  * `core`: typo fixes to log messages
  * `tcp`: stun fixes
  * `mem`: added faster malloc
  * `module_name`: support for foo rfc extension
  * `lib_name`: critical bug fix for abc case
  * `kamctl`: added support for management of module xyz

#### Examples Of Commit Messages ####

  * change to usrloc module from modules

```
usrloc: fixed name conflict

- destroy_avps() renamed to reg_destroy_avps() to avoid conflicts
  with the usr_avp.h version
```

  * change to core

```
core: loadpath can now use a list of directories

- loadpath can use a list of directories separated by ':',
  e.g.: loadpath "modules:modules_s:modules_k".
  First match wins (e.g. for loadmodule "textops" if
  modules/textops.so or modules/textops/textops.so exists, it will
  be loaded and the search will stop).
```

#### See Also ####

  * [Creating Good Commit Messages](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html#creating-good-commit-messages)
  * http://www.tpope.net/node/106

The above content about commit message format is taken from Kamailio wiki page:
  * https://www.kamailio.org/wiki/devel/git-commit-guidelines
  * it is recommended you read that one as well.

## Reporting Issues ##

Whenever reporting an issue, along with the description of the problems, try to
include following details:

  * kamailio version you are using
    * the output of: **kamailio -v**
  * the operating system being used
  * the CPU architecture

Always useful to have:

  * whenever there is a crash with a corefile, send the backtrace
    * the output of **bt full** in **gbd**
  * log messages printed by kamailio in syslog file
  * *pcap* or *ngrep* capture of SIP packets causing the issue
  * config file snippets which expose the issues

Note: replace any sensitive information in the content you add to the issue
(e.g., passwords in modparams can be replaced with xyz, each IP address can be
replaced with tokens like a.b.c.d, f.g.h.j).

## License ##

Kamailio Main License: *GPLv2*.

Each source code file refers to the license and copyright details in the top
of the file. Most of the code is licensed under GPLv2, some parts of the code
are licensed under BSD.

### License Of New Code Contributions ###

New contributions to the core and several main modules (auth, corex, sl, tls,
tm) have to be done under the BSD license. New contributions under the GPL must
grant the GPL-OpenSSL linking exception. Contributions to existing components
released under BSD must be done under BSD as well.

## Further Assistance ###

For any question, do not hesitate to contact other developers via mailing list:

  * **[sr-dev [at] lists.kamailio.org](http://lists.kamailio.org/cgi-bin/mailman/listinfo/sr-dev)**
