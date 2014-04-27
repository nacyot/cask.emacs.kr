---
title: Usage
layout: default
permalink: usage.html
---

## Usage

---

Start off by creating a file called `Cask` in the project root. Use
the `init` command to create a `Cask`-file automatically, containing
boilerplate code.

{% highlight bash %}
$ cask init [--dev]
{% endhighlight %}

_(Use `--dev` if the project is for package development)_

If you are using Cask for your Emacs configuration, add this to your
`.emacs` file:

{% highlight cl %}
(require 'cask "~/.cask/cask.el")
(cask-initialize)
{% endhighlight %}

To install all dependencies, run:

{% highlight bash %}
$ cask [install]
{% endhighlight %}

This will create a directory called `.cask`, containing all dependencies.

The commands below execute using the `emacs` binary. To specify a
custom Emacs, use the `EMACS` environment variable, for example:

{% highlight bash %}
$ EMACS="$(evm bin emacs-24.1)" cask command
{% endhighlight %}

## Commands & Options

Cask's commands and options are briefly described below. For full
documentation, use `cask help`.

* [exec](#exec)
* [help, --help, -h](#help)
* [info](#info)
* [init](#init)
* [install](#install)
* [list](#list)
* [load-path](#load-path)
* [outdated](#outdated)
* [pkg-file](#pkg-file)
* [package-directory](#package-directory)
* [path](#path)
* [update](#update)
* [upgrade-cask](#upgrade-cask)
* [version](#version)
* [files](#files)
* [build](#build)
* [clean-elc](#clean-elc)
* [link](#link)
* [package](#package)
* [--version](#option-version)
* [--dev](#option-dev)
* [--debug](#option-debug)
* [--path](#option-path)
* [--verbose](#option-verbose)

### Commands

---

#### <a id="exec"></a>exec

Execute command with correct `PATH` (see [path](#path)) and
`EMACSLOADPATH` (see [load-path](#load-path)) set up.

{% highlight bash %}
$ cask exec echo foo
$ cask exec ecukes --script --reporter gangsta
$ cask exec ert-runner --pattern performance
{% endhighlight %}

#### <a id="help"></a>help, --help, -h

Show Cask usage information.

{% highlight bash %}
$ cask help
$ cask -h
$ cask --help
$ cask --help command
{% endhighlight %}

#### <a id="info"></a>info

Show information about the project, such as name, description and
version.

{% highlight bash %}
$ cask info
{% endhighlight %}

#### <a id="init"></a>init

Create new `Cask`-file. If the project is for package development, use
the `--dev` option.

{% highlight bash %}
$ cask init       # For Emacs configuration
$ cask init --dev # For package development
{% endhighlight %}

#### <a id="install"></a>install

This is the default command, which installs all runtime and
development dependencies specified in the `Cask`-file.

{% highlight bash %}
$ cask
$ cask install
{% endhighlight %}

#### <a id="list"></a>list

List all runtime and development dependencies.

{% highlight bash %}
$ cask list
{% endhighlight %}

#### <a id="load-path"></a>load-path

Print `EMACSLOADPATH`-friendly string with path to all dependencies to
this project.

The [exec](#exec) command includes the output of this command
automatically. This means that if the command executed is an Emacs
process, there's no hassle with the `load-path`, just require the
dependencies.

{% highlight bash %}
$ cask load-path
{% endhighlight %}

#### <a id="outdated"></a>outdated

Show list of all outdated dependencies. That is dependencies that have
a more recent version available for installation.

{% highlight bash %}
$ cask outdated
{% endhighlight %}

#### <a id="package"></a>package

Create a `-pkg.el` file (see
<http://www.gnu.org/software/emacs/manual/html_node/elisp/Multi_002dfile-Packages.html#Multi_002dfile-Packages>).

{% highlight bash %}
$ cask package
{% endhighlight %}

#### <a id="package-directory"></a>package-directory

Print path to package directory, that is the path to the directory
where all dependencies are installed (`.cask/EMACS-VERSION/elpa`).

{% highlight bash %}
$ cask package-directory
{% endhighlight %}

#### <a id="path"></a>path

Print `PATH` and prepend path to all directories called `bin` in this
projects dependencies.

For example if this project depends on `ecukes`, this command will
include `.cask/EMACS-VERSION/elpa/ecukes-VERSION/bin`.

{% highlight bash %}
$ cask path
{% endhighlight %}

#### <a id="update"></a>update

Update all dependencies.

{% highlight bash %}
$ cask update
{% endhighlight %}

#### <a id="upgrade-cask"></a>upgrade-cask

Upgrade Cask and all its dependencies.

{% highlight bash %}
$ cask upgrade-cask
{% endhighlight %}

#### <a id="version"></a>version

Print version of this package.

{% highlight bash %}
$ cask version
{% endhighlight %}

#### <a id="files"></a>files

Print list of package files.

{% highlight bash %}
$ cask files
{% endhighlight %}

#### <a id="build"></a>build

Byte compile all package files. The `.elc` files are placed in the
same directory as the source file.

{% highlight bash %}
$ cask build
{% endhighlight %}

#### <a id="clean-elc"></a>clean-elc

Remove byte compiled files generated from the `build` command.

{% highlight bash %}
$ cask clean-elc
{% endhighlight %}

#### <a id="link"></a>link

Handle package links.

{% highlight bash %}
$ cask link list                 # List all links
$ cask link ecukes ~/Code/ecukes # Create link to local Ecukes
$ cask link delete ecukes        # Delete Ecukes link
{% endhighlight %}

#### <a id="package"></a>package

Build a package (`.el` or `.tar`) and place in the `dist` (or
specified) directory.

{% highlight bash %}
$ cask package
$ cask package /path/to/dist
{% endhighlight %}

### Options

---

#### <a id="option-version"></a>--version

Print Cask's version.

{% highlight bash %}
$ cask --version
{% endhighlight %}

#### <a id="option-dev"></a>--dev

Perform action in development mode. This option does only take affect
for some commands. See resp. command for that information.

{% highlight bash %}
$ cask --dev
{% endhighlight %}

#### <a id="option-debug"></a>--debug

Enable debug information.

{% highlight bash %}
$ cask --debug
{% endhighlight %}

#### <a id="option-path"></a>--path

Change default directory to path before executing command.

{% highlight bash %}
$ cask --path /path/to
{% endhighlight %}

#### <a id="option-verbose"></a>--verbose

Cask tries to hide as much output as possible by default. With this
option, all output will show.

{% highlight bash %}
$ cask install --verbose
{% endhighlight %}
