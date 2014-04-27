---
title: DSL
layout: default
permalink: dsl.html
---

## DSL

---

* [source](#source)
* [package](#package)
* [package-file](#package-file)
* [depends-on](#depends-on)
* [development](#development)
* [files](#files)

---

#### <a id="source"></a>source

Add a package mirror.

{% highlight cl %}
(source ALIAS)
(source NAME URL)
{% endhighlight %}

Example:

{% highlight cl %}
(source melpa)
(source "melpa" "http://melpa.milkbox.net/packages/")
{% endhighlight %}

Available aliases:

 * `gnu` (<http://elpa.gnu.org/packages/>)
 * `melpa` (<http://melpa.milkbox.net/packages/>)
 * `marmalade` (<http://marmalade-repo.org/packages/>)
 * `SC` (<http://joseito.republika.pl/sunrise-commander/>)
 * `org` (<http://orgmode.org/elpa/>)

#### <a id="package"></a>package

Define this package (used only for package development).

{% highlight cl %}
(package NAME VERSION DESCRIPTION)
{% endhighlight %}

Example:

{% highlight cl %}
(package "ecukes" "0.2.1" "Cucumber for Emacs.")
{% endhighlight %}

#### <a id="package-file"></a>package-file

Define this package and its runtime dependencies from the package
headers of a file (used only for package development). The name of the
file is relative to the directory containing the `Cask` file.

{% highlight cl %}
(package-file FILENAME)
{% endhighlight %}

Example:

{% highlight cl %}
(package-file "foo.el")
{% endhighlight %}

#### <a id="depends-on"></a>depends-on

Add a dependency.

{% highlight cl %}
(depends-on NAME [ARGS])
{% endhighlight %}

Example:

{% highlight cl %}
(depends-on "ecukes")
(depends-on "magit" "0.8.1")
(depends-on "magit" :git "https://github.com/magit/magit.git")
(depends-on "magit" :git "https://github.com/magit/magit.git" :ref "7j3bj4d")
(depends-on "magit" :git "https://github.com/magit/magit.git" :branch "next")
(depends-on "magit" :git "https://github.com/magit/magit.git" :files ("*.el" (:exclude "magit-svn.el")))
{% endhighlight %}

#### <a id="development"></a>development

Set scope to development.

{% highlight cl %}
(development [DEPENDENCIES])
{% endhighlight %}

Example:

{% highlight cl %}
(development
 (depends-on "ecukes")
 (depends-on "ert-runner"))
{% endhighlight %}

#### <a id="files"></a>files

Specify list of files that are included in this project.

{% highlight cl %}
(files [FILES])
{% endhighlight %}

Example:

{% highlight cl %}
(files "foo.el")
(files "foo.el" "foo-core.el")
{% endhighlight %}
