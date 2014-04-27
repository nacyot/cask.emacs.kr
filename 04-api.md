---
title: API
layout: default
permalink: api.html
---

## API

---

이 문서는 Cask 확장 API를 간략히 설명합니다. 각 함수에 대한 자세한 설명은 doc-string을 읽어주세요.

아래에서 보이듯이 모든 함수는 첫번째 인자로 `bundle`을 받습니다. 번들이란 현재 Cask 프로젝트를 의미합니다. 번들 객체를 직접 조작하지 마세요. API 함수들을 이용해서 조작하시기 바랍니다.

`bundle` 객체를 처음 만드려면 `cask-setup`이나 `cask-initialize` 함수를 사용할 수 있습니다.

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

### 문서와 예제

#### <a id="cask-setup"></a>cask-setup `(project-path)`

`project-path`에  `bundle` 객체를 생성합니다. `cask-setup`은 패키지를 관리하는데 사용합니다. Emacs 설정을 할 때는 `cask-initialize`을 사용하세요.

{% highlight cl %}
(let ((bundle (cask-setup "/path/to/project")))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-initialize"></a>cask-initialize `(&optional project-path)`

`cask-setup`와 비슷한 기능을 하지만 추가적으로 모든 의존 라이브러리를 초기화합니다. `cask-initialize`는 Emacs를 설정할 때 사용합니다. 패키지를 만들 때는 `cask-setup`을 사용하세요.

{% highlight cl %}
(let ((bundle (cask-initialize "/path/to/project")))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-update"></a>cask-update `(bundle)`

의존 라이브러리를 업데이트하고 업데이트된 의존 라이브러리의 리스트를 출력합니다.

{% highlight cl %}
(let ((updated (cask-update bundle)))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-outdated"></a>cask-outdated `(bundle)`

최신 버전이 아닌 모든 의존 라이브러리의 목록을 리턴합니다.

{% highlight cl %}
(let ((outdated (cask-outdated bundle)))
  ;; ...
  )
{% endhighlight %}

#### <a id="cask-install"></a>cask-install `(bundle)`

의존 라이브러리를 설치합니다.

{% highlight cl %}
(cask-install bundle)
{% endhighlight %}

#### <a id="cask-caskify"></a>cask-caskify `(bundle &optional dev-mode)`

`Cask` 파일을 생성합니다.

{% highlight cl %}
(cask-caskify bundle)           ;; For Emacs configuration
(cask-caskify bundle 'dev-mode) ;; For packages
{% endhighlight %}

#### <a id="cask-package-name"></a>cask-package-name `(bundle)`

패키지 이름을 리턴합니다.

{% highlight cl %}
(cask-package-name bundle) ;; => 'foo
{% endhighlight %}

#### <a id="cask-package-version"></a>cask-package-version `(bundle)`

패키지 버전을 리턴합니다.

{% highlight cl %}
(cask-package-version bundle) ;; => "0.1.2"
{% endhighlight %}

#### <a id="cask-package-description"></a>cask-package-description `(bundle)`

패키지 설명을 리턴합니다.

{% highlight cl %}
(cask-package-description bundle) ;; => "Description for Foo package"
{% endhighlight %}

#### <a id="cask-version"></a>cask-version `()`

Cask 버전을 리턴합니다.

{% highlight cl %}
(cask-version)
{% endhighlight %}

#### <a id="cask-load-path"></a>cask-load-path `(bundle)`

의존 라이브러리가 있는 `load-path`를 리턴합니다.

{% highlight cl %}
(cask-load-path bundle) ;; => '("/path/to/.cask/24.3.1/elpa/foo-1.2.3" ...)
{% endhighlight %}

#### <a id="cask-exec-path"></a>cask-exec-path `(bundle)`

의존 라이브러리가 있는 `exec-path`를 리턴합니다.

{% highlight cl %}
(cask-exec-path bundle) ;; => '("/path/to/.cask/24.3.1/elpa/foo-1.2.3/bin" ...)
{% endhighlight %}

#### <a id="cask-elpa-path"></a>cask-elpa-path `(bundle)`

elpa 디렉토리 경로를 리턴합니다.

{% highlight cl %}
(cask-elpa-path bundle) ;; => "/path/to/.cask/24.3.1/elpa"
{% endhighlight %}

#### <a id="cask-runtime-dependencies"></a>cask-runtime-dependencies `(bundle &optional deep)`

런타임 의존 라이브러리 목록을 리턴합니다.

{% highlight cl %}
(cask-runtime-dependencies bundle)
(cask-runtime-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-development-dependencies"></a>cask-development-dependencies `(bundle &optional deep)`

개발 의존 라이브러리의 목록을 리턴합니다.

{% highlight cl %}
(cask-development-dependencies bundle)
(cask-development-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-dependencies"></a>cask-dependencies `(bundle &optional deep)`

런타임 의존 라이브러리와 개발 의존 라이브러리 전체 목록을 리턴합니다.

{% highlight cl %}
(cask-dependencies bundle)
(cask-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-installed-dependencies"></a>cask-installed-dependencies `(bundle &optional deep)`

현재 설치된 의존 라이브러리 목록을 리턴합니다.

{% highlight cl %}
(cask-installed-dependencies bundle)
(cask-installed-dependencies bundle 'deep)
{% endhighlight %}

#### <a id="cask-has-dependency"></a>cask-has-dependency `(bundle name)`

프로젝트가 `name`이라는 라이브러리에 의존성이 있으면 true를 리턴합니다.

{% highlight cl %}
(cask-has-dependency bundle 'foo)
{% endhighlight %}

#### <a id="cask-find-dependency"></a>cask-find-dependency `(bundle name)`

`name`으로 검색된 의존 라이브러리를 리턴합니다.

{% highlight cl %}
(cask-find-dependency bundle 'foo)
{% endhighlight %}

#### <a id="cask-define-package-string"></a>cask-define-package-string `(bundle)`

`-pkg.el`에서 사용하는 `define-package` 문자열을 리턴합니다.

{% highlight cl %}
(cask-define-package-string bundle) ;; => "(define-package ...)"
{% endhighlight %}

#### <a id="cask-define-package-file"></a>cask-define-package-file `(bundle)`

`-pkg.el` 파일의 경로를 리턴합니다.

{% highlight cl %}
(cask-define-package-file bundle) ;; => "/path/to/project-pkg.el"
{% endhighlight %}

#### <a id="cask-dependency-path"></a>cask-dependency-path `(bundle name)`

`name`이라는 이름을 가진 의존 라이브러리의 경로를 리턴합니다.

{% highlight cl %}
(cask-dependency-path bundle 'foo) ;; => "/path/to/.cask/24.3.1/elpa/foo-1.3.3"
{% endhighlight %}

#### <a id="cask-path"></a>cask-path `(bundle)`

프로젝트 루트 디렉토리 경로를 리턴합니다.

{% highlight cl %}
(cask-path bundle) ;; => "/path/to"
{% endhighlight %}

#### <a id="cask-file"></a>cask-file `(bundle)`

`Cask`-file의 경로를 리턴합니다.

{% highlight cl %}
(cask-file bundle) ;; => "/path/to/Cask"
{% endhighlight %}

#### <a id="cask-files"></a>cask-files `(bundle)`

프로젝트 파일들의 목록을 리턴합니다.

{% highlight cl %}
(cask-files bundle) ;; => '("foo.el" "foo-core.el" ...)
{% endhighlight %}

#### <a id="cask-add-dependency"></a>cask-add-dependency `(bundle name &rest args)`

`name`이라는 이름을 가진 의존 라이브러리를 추가합니다.

마지막 인자인 `args`에는 아래와 같은 것들이 들어갈 수 있습니다.

* 최소 버전을 지정하는 문자열* VCS fetcher 옵션을 지정하는 plist  * `:ref` - 체크아웃하고자 하는 Fetcher ref.
  * `:branch` - 체크아웃 하고자 하는 Fetcher 브랜치  * `:files` - 가져올 파일의 패턴(이 패턴에 일치하는 파일만 가져옵니다)

{% highlight cl %}
(cask-add-dependency bundle 'foo)
(cask-add-dependency bundle 'foo "1.2.3")
(cask-add-dependency bundle 'foo :git "https://foo.git" :ref "ij7ads0" :files '("*.el" (:exclude ".git")))
(cask-add-dependency bundle 'foo :git "https://foo.git" :branch "experimental")
{% endhighlight %}

#### <a id="cask-add-source"></a>cask-add-source `(bundle name-or-alias &optional url)`

ELPA 소스를 추가합니다.

{% highlight cl %}
(cask-add-dependency bundle "name" "http://path.to.elpa/packages/")
(cask-add-dependency bundle 'alias)
{% endhighlight %}

#### <a id="cask-remove-source"></a>cask-remove-source `(bundle name)`

ELPA 소스를 삭제합니다.

{% highlight cl %}
(cask-remove-dependency bundle "name")
{% endhighlight %}

#### <a id="cask-build"></a>cask-build `(bundle)`

프로젝트 파일을 바이트 컴파일합니다.

{% highlight cl %}
(cask-build bundle)
{% endhighlight %}

#### <a id="cask-clean-elc"></a>cask-clean-elc `(bundle)`

바이트 컴파일된 파일을 삭제합니다.

{% highlight cl %}
(cask-clean-elc bundle)
{% endhighlight %}

#### <a id="cask-links"></a>cask-links `(bundle)`

링크 목록을 리턴합니다.

{% highlight cl %}
(cask-links bundle) ;; => '((foo "/path/to/too") (bar "/path/to/bar"))
{% endhighlight %}

#### <a id="cask-link"></a>cask-link `(bundle name source)`

`name`에서 `source` 경로를 향하는 링크를 생성합니다.

{% highlight cl %}
(cask-link bundle 'foo "/path/to/foo")
{% endhighlight %}

#### <a id="cask-link-delete"></a>cask-link-delete `(bundle name)`

`name` 이름을 가진 링크를 삭제합니다.

{% highlight cl %}
(cask-delete-link bundle 'foo)
{% endhighlight %}

#### <a id="cask-linked-p"></a>cask-linked-p `(bundle name)`

`name` 이름을 가진 링크가 있으면 true를 리턴하고, 그렇지 않으면 false를 리턴합니다.

{% highlight cl %}
(cask-linked-p bundle 'foo)
{% endhighlight %}

#### <a id="cask-package"></a>cask-package `(bundle &optional target-dir)`

현재 프로젝트를 ELPA 패키지로 만듭니다. 패키지를 `dist` 디렉토리로 옮기거나 `target-dir`가 지정되어 있으면 `target-dir`로 옮깁니다.

{% highlight cl %}
(cask-package bundle)
(cask-package bundle "/path/to/dist")
{% endhighlight %}

