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

패키지 미러를 추가합니다.

{% highlight cl %}
(source ALIAS)
(source NAME URL)
{% endhighlight %}

예제:

{% highlight cl %}
(source melpa)
(source "melpa" "http://melpa.milkbox.net/packages/")
{% endhighlight %}

사용가능한 미러의 약어는 아래와 같습니다.

 * `gnu` (<http://elpa.gnu.org/packages/>)
 * `melpa` (<http://melpa.milkbox.net/packages/>)
 * `marmalade` (<http://marmalade-repo.org/packages/>)
 * `SC` (<http://joseito.republika.pl/sunrise-commander/>)
 * `org` (<http://orgmode.org/elpa/>)

#### <a id="package"></a>package

패키지를 정의합니다.(패키지 개발에서만 사용됩니다)

{% highlight cl %}
(package NAME VERSION DESCRIPTION)
{% endhighlight %}

예제:

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

예제:

{% highlight cl %}
(package-file "foo.el")
{% endhighlight %}

#### <a id="depends-on"></a>depends-on

의존 라이브러리를 추가합니다.

{% highlight cl %}
(depends-on NAME [ARGS])
{% endhighlight %}

예제:

{% highlight cl %}
(depends-on "ecukes")
(depends-on "magit" "0.8.1")
(depends-on "magit" :git "https://github.com/magit/magit.git")
(depends-on "magit" :git "https://github.com/magit/magit.git" :ref "7j3bj4d")
(depends-on "magit" :git "https://github.com/magit/magit.git" :branch "next")
(depends-on "magit" :git "https://github.com/magit/magit.git" :files ("*.el" (:exclude "magit-svn.el")))
{% endhighlight %}

#### <a id="development"></a>개발

의존 라이브러리를 개발 시에만 사용하도록 설정합니다.

{% highlight cl %}
(development [DEPENDENCIES])
{% endhighlight %}

예제:

{% highlight cl %}
(development
 (depends-on "ecukes")
 (depends-on "ert-runner"))
{% endhighlight %}

#### <a id="files"></a>files

이 프로젝트에 포함되는 파일을 명시합니다.

{% highlight cl %}
(files [FILES])
{% endhighlight %}

예제:

{% highlight cl %}
(files "foo.el")
(files "foo.el" "foo-core.el")
{% endhighlight %}
