---
title: 사용법
layout: default
permalink: usage.html
---

## 사용법

---

우선 `Cask` 파일을 Emacs Lisp 프로젝트 루트에 만들어야합니다. `init` 명령어를 통해 간단한 골격을 포함한 `Cask` 파일을 자동으로 생성할 수 있습니다.

{% highlight bash %}
$ cask init [--dev]
{% endhighlight %}

_(`--dev` 옵션은 개발 모드로 Cask를 실행할 때 사용합니다)_

Emacs 설정을 위해 Cask를 사용하고자 할 때는 아래 내용을 `.emacs`에 추가해줍니다.

{% highlight cl %}
(require 'cask "~/.cask/cask.el")
(cask-initialize)
{% endhighlight %}

모든 의존 라이브러리를 설치하려면 아래 명령어를 실행하세요.

{% highlight bash %}
$ cask [install]
{% endhighlight %}

이 명령어는 `.cask` 디렉토리를 만들고 모든 의존 라이브러리를 설치합니다.

이 명령어는 `emacs`를 사용해서 실행됩니다. 따라서 특정한 버전의 Emacs를 사용하고자 할 때는 `EMACS` 환경변수를 아래와 같이 지정합니다.

{% highlight bash %}
$ EMACS="$(evm bin emacs-24.1)" cask command
{% endhighlight %}

## 명령어와 옵션

아래에서는 Cask의 명령과 옵션에 대해서 간략히 소개합니다. 전체 문서는 `cask help` 명령어를 통해서 확인해주세요.

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

### 명령어

---

#### <a id="exec"></a>exec

exec 명령어를 사용할 때는 `PATH`([path](#path) 참조)와 `EMACSLOADPATH`([load-path](#load-path) 환경변수를 올바르게 설정해야합니다.

{% highlight bash %}
$ cask exec echo foo
$ cask exec ecukes --script --reporter gangsta
$ cask exec ert-runner --pattern performance
{% endhighlight %}

#### <a id="help"></a>help, --help, -h

Cask 사용법을 출력합니다.

{% highlight bash %}
$ cask help
$ cask -h
$ cask --help
$ cask --help command
{% endhighlight %}

#### <a id="info"></a>info

특정 프로젝트의 이름, 설명, 버전과 같은 정보를 출력합니다.

{% highlight bash %}
$ cask info
{% endhighlight %}

#### <a id="init"></a>init

새로운 `Cask` 파일을 생성합니다. 패키지 개발 용도로 사용한다면 `--dev` 옵션을 사용해주세요.

{% highlight bash %}
$ cask init       # For Emacs configuration
$ cask init --dev # For package development
{% endhighlight %}

#### <a id="install"></a>install

이는 Cask의 기본 명령어로 모든 런타임과 `Cask`에 정의된 개발에 의존된 라이브러를 전부 설치합니다.

{% highlight bash %}
$ cask
$ cask install
{% endhighlight %}

#### <a id="list"></a>list

모든 런타임과 개발에 의존된 라이브러리 목록을 출력합니다.

{% highlight bash %}
$ cask list
{% endhighlight %}

#### <a id="load-path"></a>load-path

현재 프로젝트가 의존하고 있는 모든 라이브러리들의 경로를 `EMACSLOADPATH` 환경변수에서 사용가능한 문자열로 출력해줍니다.

[exec](#exec) 명령어를 사용할 때 `load-path` 명령어에서 출력되는 경로들을 참조합니다. 즉 emacs와 관련된 명령어를 실행할 때 `load-path`에 대해 고민하지 않아도 됩니다. 의존 라이브러리 추가만 하면 해당하는 라이브러리의 경로는 cask가 알아서 추가해줍니다. 

{% highlight bash %}
$ cask load-path
{% endhighlight %}

#### <a id="outdated"></a>outdated

오래된 의존 라이브러리 리스트를 전부 출력합니다. 오래된 의존 라이브러리란 최신 버전으로 업그레이드 가능한 설치되어있는 라이브러리를 의미합니다.

{% highlight bash %}
$ cask outdated
{% endhighlight %}

#### <a id="package"></a>package

`-pkg.el` 파일을 생성합니다. (
<http://www.gnu.org/software/emacs/manual/html_node/elisp/Multi_002dfile-Packages.html#Multi_002dfile-Packages>를 참조하세요).

{% highlight bash %}
$ cask package
{% endhighlight %}

#### <a id="package-directory"></a>package-directory

모든 의존 라이브러리가 설치되는 디렉토리 경로를 출력합니다.(`.cask/EMACS-VERSION/elpa`)

{% highlight bash %}
$ cask package-directory
{% endhighlight %}

#### <a id="path"></a>path

`PATH`를 출력하고 의존 라이브러리의 모든 `bin` 디렉토리를 출력합니다.

예를 들어 프로젝트가 `ecukes`에 의존하고 있다면 이 명령어는 `.cask/EMACS-VERSION/elpa/ecukes-VERSION/bin`를 포함합니다.

{% highlight bash %}
$ cask path
{% endhighlight %}

#### <a id="update"></a>update

모든 의존 라이브러리를 업데이트합니다.

{% highlight bash %}
$ cask update
{% endhighlight %}

#### <a id="upgrade-cask"></a>upgrade-cask

Cask와 의존 라이브러리를 업그레이드합니다.

{% highlight bash %}
$ cask upgrade-cask
{% endhighlight %}

#### <a id="version"></a>version

패키지의 버전을 출력합니다.

{% highlight bash %}
$ cask version
{% endhighlight %}

#### <a id="files"></a>files

패키지 파일 리스트를 출력합니다.

{% highlight bash %}
$ cask files
{% endhighlight %}

#### <a id="build"></a>build

모든 패키지 파일을 바이트 컴파일 합니다. 모든 `.elc` 파일은 source 디렉토리와 같은 곳에 위치합니다.

{% highlight bash %}
$ cask build
{% endhighlight %}

#### <a id="clean-elc"></a>clean-elc

`build` 명령어로 만들어진 바이트 컴파일 파일들을 삭제합니다.

{% highlight bash %}
$ cask clean-elc
{% endhighlight %}

#### <a id="link"></a>link

패키지 링크를 관리합니다.

{% highlight bash %}
$ cask link list                 # List all links
$ cask link ecukes ~/Code/ecukes # Create link to local Ecukes
$ cask link delete ecukes        # Delete Ecukes link
{% endhighlight %}

#### <a id="package"></a>package

`.el`이나 `.tar`로 된 패키지를 생성하고 `dist` 디렉토리에 복사합니다.

{% highlight bash %}
$ cask package
$ cask package /path/to/dist
{% endhighlight %}

### 옵션

---

#### <a id="option-version"></a>--version

Cask의 버전을 출력합니다.

{% highlight bash %}
$ cask --version
{% endhighlight %}

#### <a id="option-dev"></a>--dev

명령어를 개발 모드(development mode)로 실행합니다. 이 옵션이 모든 명령어에 적용되지는 않습니다. 각각의 명령어 설명을 읽어주세요.

{% highlight bash %}
$ cask --dev
{% endhighlight %}

#### <a id="option-debug"></a>--debug

디버그 정보를 출력합니다.

{% highlight bash %}
$ cask --debug
{% endhighlight %}

#### <a id="option-path"></a>--path

명령어를 실행하기 전에 작업 디렉토리를 path 옵션에 지정한 곳으로 변경합니다.

{% highlight bash %}
$ cask --path /path/to
{% endhighlight %}

#### <a id="option-verbose"></a>--verbose

Cask는 출력사항이 많을 때 기본적으로 이를 최대한 숨겨줍니다. 이 옵션을 사용하면 숨기는 내용없이 모든 내용이 출력됩니다.

{% highlight bash %}
$ cask install --verbose
{% endhighlight %}
