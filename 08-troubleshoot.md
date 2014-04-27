---
title: Troubleshoot
layout: default
permalink: troubleshoot.html
---

## Troubleshoot

---

### Error running a Cask command

If you run a Cask command and get an error, there are a few things you
can try yourself.

First, make sure you have the latest Cask version (Run `cask
--version` to find out what version you are using). Upgrade Cask and
its dependencies using `cask upgrade-cask` (avoid upgrading using `git
pull` or similar).

If the error still occurs, try removing Cask's dependencies. They are
located in `~/.emacs.d/.cask/EMACS-VERSION/bootstrap`. Remove that
directory and try again.

Still doesn't work? [Create an issue](github.com/cask/cask/issues/new)
and we will help you. Please run any command with the options
`--verbose` and `--debug` to give us as much information as possible.
