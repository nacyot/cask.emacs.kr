---
title: Why Cask?
layout: default
permalink: why-cask.html
---

## Why Cask?

---

This document explains why you should use Cask, both in your Emacs
configuration and for Emacs Lisp package development.

### Emacs Lisp package development

So, why should your Emacs Lisp project use Cask? Do you know why:

* Ruby projects have a `gemspec` file?
* Node.js projects have a `package.json` file?
* Clojure projects have a `project.clj` file?
* Emacs Lisp projects have a `Cask` file?

Actually, let me rephrase the last statement.

* Some Emacs Lisp projects have a `Cask` file?

No, let's try that again.

* Some Emacs Lisp projects does not have a `Cask` file?

I will argue that some Emacs Lisp projects may not benefit directly
from using Cask. Those are the projects that:

* Does not have any dependencies
* Does not have any tests
* Does not care about consistency
* Does not care about compiler warnings
* Does not want to make it easy for contributors

So all in all, projects that are not worth using.

Emacs package development has improved drastically during the last
couple of years. From single Emacs Lisp files uploaded to the Emacs
Wiki, to high quality packages, using VCS, that are tested,
installable via a package manager and more.

But there's one thing still missing and that is consistency. Note that
*every* Ruby project has a `gemspec` file, *every* Node.js project has
a `package.json` file and *every* Clojure project has a `project.clj`
file.

In those environments, projects are structured, tested, packaged,
compiled, released in the same way. If you find a new project and want
to find out what dependencies it has, you will know exactly where to
look. If you want to find the test for a specific feature, you know
exactly where to look.

For Emacs Lisp projects using Cask, this is true as well.

So, even if you feel that your Emacs Lisp project does not have direct
benefit of using Cask, please do so any way. If not for you, do it for
other Emacs Lisp developers.

### Emacs configuration

If you look at the majority of Emacs configurations out there, you
will see a few different types setups. These are the major ones:

#### El-get

El-get is popular because is was created when there were no other good
alternatives. Now there are and `package.el` is the standard solution,
choosen by the Emacs core developers. El-get did a good job once, but
is nowadays obsolete. Let's keep to the standard way of doing things!

#### Using package.el directly

It usually looks something like this:

{% highlight cl %}
(require 'package)
(package-initialize)
(mapc
 (lambda (package)
   (unless (package-installed-p package)
     (package-install package)))
 '(s f dash flycheck prodigy ...))
{% endhighlight %}

I did something like this in my configuration once as well, but I no
longer have to, because Cask exists.

#### Submodules

I have over 60 packages in my Emacs configuration. Can you imagine how
much work it would require to keep all of those up to date?

#### Bundled packages

This has the same "keeping up to date" issue as the submodules
approach. But it's even worse. Storing dependencies as part of the
repository is madness. I shouldn't have to explain why.

#### Cask

This is obviously what we want. All it is, is a single file that
declares a list of dependencies. You know where to look if you want to
find out what dependencies a configuration has and it's easy to keep
packages up to date.
