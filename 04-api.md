---
title: API
layout: default
permalink: api.html
---

## API

---

Cask has an extensive API, which is briefly described in this
document. For full documentation of each function, read the function
doc-string.

As you will see, almost every API function takes a `bundle` as first
argument. A bundle is an object that describes the current Cask
project. You should not modify this object directly, but use the API
functions to do so.

To create a `bundle` object, use either `cask-setup` or
`cask-initialize`, which are described below.

* [cask-setup](#cask-setup) `(project-path)`
* [cask-initialize](#cask-initialize) `(&optional project-path)`
* [cask-update](#cask-update) `(bundle)`
* [cask-outdated](#cask-outdated) `(bundle)`
* [cask-install](#cask-install) `(bundle)`
* [cask-caskify](#cask-caskify) `(bundle &optional dev-mode)`
* [cask-package-name](#cask-package-name) `(bundle)`
* [cask-package-version](#cask-package-version) `(bundle)`
* [cask-package-description](#cask-package-description) `(bundle)`
* [cask-version](#cask-version) `()`
* [cask-load-path](#cask-load-path) `(bundle)`
* [cask-exec-path](#cask-exec-path) `(bundle)`
* [cask-elpa-path](#cask-elpa-path) `(bundle)`
* [cask-runtime-dependencies](#cask-runtime-dependencies) `(bundle &optional deep)`
* [cask-development-dependencies](#cask-development-dependencies) `(bundle &optional deep)`
* [cask-dependencies](#cask-dependencies) `(bundle &optional deep)`
* [cask-installed-dependencies](#cask-installed-dependencies) `(bundle &optional deep)`
* [cask-has-dependency](#cask-has-dependency) `(bundle name)`
* [cask-find-dependency](#cask-find-dependency) `(bundle name)`
* [cask-define-package-string](#cask-define-package-string) `(bundle)`
* [cask-define-package-file](#cask-define-package-file) `(bundle)`
* [cask-dependency-path](#cask-dependency-path) `(bundle name)`
* [cask-path](#cask-path) `(bundle)`
* [cask-file](#cask-file) `(bundle)`
* [cask-files](#cask-files) `(bundle)`
* [cask-add-dependency](#cask-add-dependency) `(bundle name &rest args)`
* [cask-add-source](#cask-add-source) `(bundle name-or-alias &optional url)`
* [cask-remove-source](#cask-remove-source) `(bundle name)`
* [cask-build](#cask-build) `(bundle)`
* [cask-clean-elc](#cask-clean-elc) `(bundle)`
* [cask-links](#cask-links) `(bundle)`
* [cask-link](#cask-link) `(bundle name source)`
* [cask-link-delete](#cask-link-delete) `(bundle name)`
* [cask-linked-p](#cask-linked-p) `(bundle name)`
* [cask-package](#cask-package) `(bundle &optional target-dir)`

### Documentation and Examples

#### <a id="cask-setup"></a>cask-setup `(project-path)`

Create a `bundle` object for `project-path`. Use this function for
packages and `cask-initialize` for your local Emacs configuration.

{% highlight cl %}
(let ((bundle (cask-setup "/path/to/project")))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-initialize"></a>cask-initialize `(&optional project-path)`

Like `cask-setup`, but also initializes all dependencies. Use this
function for your local Emacs configuration and `cask-setup` for
packages.

{% highlight cl %}
(let ((bundle (cask-initialize "/path/to/project")))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-update"></a>cask-update `(bundle)`

Update dependencies and return list of updated dependencies.

{% highlight cl %}
(let ((updated (cask-update bundle)))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-outdated"></a>cask-outdated `(bundle)`

Return a list of all outdated dependencies.

{% highlight cl %}
(let ((outdated (cask-outdated bundle)))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-install"></a>cask-install `(bundle)`

Install dependencies.

{% highlight cl %}
(cask-install bundle)
{% endhighlight %}

#### <a id="cask-caskify"></a>cask-caskify `(bundle &optional dev-mode)`

Create `Cask`-file.

{% highlight cl %}
(cask-caskify bundle)           ;; For Emacs configuration
(cask-caskify bundle 'dev-mode) ;; For packages
{% endhighlight %}

#### <a id="cask-package-name"></a>cask-package-name `(bundle)`

Return package name.

{% highlight cl %}
(cask-package-name bundle) ;; => 'foo
{% endhighlight %}

#### <a id="cask-package-version"></a>cask-package-version `(bundle)`

Return package version.

{% highlight cl %}
(cask-package-version bundle) ;; => "0.1.2"
{% endhighlight %}

#### <a id="cask-package-description"></a>cask-package-description `(bundle)`

Return package description.

{% highlight cl %}
(cask-package-description bundle) ;; => "Description for Foo package"
{% endhighlight %}

#### <a id="cask-version"></a>cask-version `()`

Return Cask's version.

{% highlight cl %}
(cask-version)
{% endhighlight %}

#### <a id="cask-load-path"></a>cask-load-path `(bundle)`

Return `load-path` including dependencies.

{% highlight cl %}
(cask-load-path bundle) ;; => '("/path/to/.cask/24.3.1/elpa/foo-1.2.3" ...)
{% endhighlight %}

#### <a id="cask-exec-path"></a>cask-exec-path `(bundle)`

Return `exec-path` including dependencies.

{% highlight cl %}
(cask-exec-path bundle) ;; => '("/path/to/.cask/24.3.1/elpa/foo-1.2.3/bin" ...)
{% endhighlight %}

#### <a id="cask-elpa-path"></a>cask-elpa-path `(bundle)`

Return path to elpa directory.

{% highlight cl %}
(cask-elpa-path bundle) ;; => "/path/to/.cask/24.3.1/elpa"
{% endhighlight %}

#### <a id="cask-runtime-dependencies"></a>cask-runtime-dependencies `(bundle &optional deep)`

Return list of runtime dependencies.

{% highlight cl %}
(cask-runtime-dependencies bundle)
(cask-runtime-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-development-dependencies"></a>cask-development-dependencies `(bundle &optional deep)`

Return list of development dependencies.

{% highlight cl %}
(cask-development-dependencies bundle)
(cask-development-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-dependencies"></a>cask-dependencies `(bundle &optional deep)`

Return list of runtime and development dependencies.

{% highlight cl %}
(cask-dependencies bundle)
(cask-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-installed-dependencies"></a>cask-installed-dependencies `(bundle &optional deep)`

Return list of installed dependencies.

{% highlight cl %}
(cask-installed-dependencies bundle)
(cask-installed-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-has-dependency"></a>cask-has-dependency `(bundle name)`

Return true if project has dependency with `name`.

{% highlight cl %}
(cask-has-dependency bundle 'foo)
{% endhighlight %}

#### <a id="cask-find-dependency"></a>cask-find-dependency `(bundle name)`

Return dependency with `name`.

{% highlight cl %}
(cask-find-dependency bundle 'foo)
{% endhighlight %}

#### <a id="cask-define-package-string"></a>cask-define-package-string `(bundle)`

Return `define-package` string used for `-pkg.el` files.

{% highlight cl %}
(cask-define-package-string bundle) ;; => "(define-package ...)"
{% endhighlight %}

#### <a id="cask-define-package-file"></a>cask-define-package-file `(bundle)`

Return path to `-pkg.el` file.

{% highlight cl %}
(cask-define-package-file bundle) ;; => "/path/to/project-pkg.el"
{% endhighlight %}

#### <a id="cask-dependency-path"></a>cask-dependency-path `(bundle name)`

Return path to dependency with `name`.

{% highlight cl %}
(cask-dependency-path bundle 'foo) ;; => "/path/to/.cask/24.3.1/elpa/foo-1.3.3"
{% endhighlight %}

#### <a id="cask-path"></a>cask-path `(bundle)`

Return path to project root.

{% highlight cl %}
(cask-path bundle) ;; => "/path/to"
{% endhighlight %}

#### <a id="cask-file"></a>cask-file `(bundle)`

Return path to project `Cask`-file.

{% highlight cl %}
(cask-file bundle) ;; => "/path/to/Cask"
{% endhighlight %}

#### <a id="cask-files"></a>cask-files `(bundle)`

Return list of project files.

{% highlight cl %}
(cask-files bundle) ;; => '("foo.el" "foo-core.el" ...)
{% endhighlight %}

#### <a id="cask-add-dependency"></a>cask-add-dependency `(bundle name &rest args)`

Add dependency with `name`.

Last argument `args`, can be:

* A string specifying minimum version.
* A plist specifying VCS fetcher options.
  * `:ref` - Fetcher ref to checkout.
  * `:branch` - Fetcher branch to checkout.
  * `:files` - Only include files matching this pattern.

{% highlight cl %}
(cask-add-dependency bundle 'foo)
(cask-add-dependency bundle 'foo "1.2.3")
(cask-add-dependency bundle 'foo :git "https://foo.git" :ref "ij7ads0" :files '("*.el" (:exclude ".git")))
(cask-add-dependency bundle 'foo :git "https://foo.git" :branch "experimental")
{% endhighlight %}

#### <a id="cask-add-source"></a>cask-add-source `(bundle name-or-alias &optional url)`

Add ELPA source.

{% highlight cl %}
(cask-add-dependency bundle "name" "http://path.to.elpa/packages/")
(cask-add-dependency bundle 'alias)
{% endhighlight %}

#### <a id="cask-remove-source"></a>cask-remove-source `(bundle name)`

Remove ELPA source.

{% highlight cl %}
(cask-remove-dependency bundle "name")
{% endhighlight %}

#### <a id="cask-build"></a>cask-build `(bundle)`

Byte compile project files.

{% highlight cl %}
(cask-build bundle)
{% endhighlight %}

#### <a id="cask-clean-elc"></a>cask-clean-elc `(bundle)`

Remove byte compiled files.

{% highlight cl %}
(cask-clean-elc bundle)
{% endhighlight %}

#### <a id="cask-links"></a>cask-links `(bundle)`

Return list of links.

{% highlight cl %}
(cask-links bundle) ;; => '((foo "/path/to/too") (bar "/path/to/bar"))
{% endhighlight %}

#### <a id="cask-link"></a>cask-link `(bundle name source)`

Create link with `name` to `source` path.

{% highlight cl %}
(cask-link bundle 'foo "/path/to/foo")
{% endhighlight %}

#### <a id="cask-link-delete"></a>cask-link-delete `(bundle name)`

Delete link with `name`.

{% highlight cl %}
(cask-delete-link bundle 'foo)
{% endhighlight %}

#### <a id="cask-linked-p"></a>cask-linked-p `(bundle name)`

Return true if link with `name` exist, false otherwise.

{% highlight cl %}
(cask-linked-p bundle 'foo)
{% endhighlight %}

#### <a id="cask-package"></a>cask-package `(bundle &optional target-dir)`

Create an ELPA package of this project. Put package in directory
called `dist` or `target-dir` if specified.

{% highlight cl %}
(cask-package bundle)
(cask-package bundle "/path/to/dist")
{% endhighlight %}

