---
title: 예제
layout: default
permalink: examples.html
---

## 예제

---

아래는 `Cask`파일 예제입니다.

### Emacs 설정

{% highlight cl %}
(source melpa)

(depends-on "auto-complete")
(depends-on "dash")
(depends-on "f")
(depends-on "flycheck")
(depends-on "helm")
(depends-on "magit")
(depends-on "popup")
(depends-on "projectile")
(depends-on "s")
(depends-on "smartparens")
(depends-on "yasnippet")
{% endhighlight %}

### 패키지 개발

{% highlight cl %}
(source melpa)

(package-file "super.el")

(files "super.el" "bin")

(development
 (depends-on "el-mock")
 (depends-on "ecukes")
 (depends-on "ert-runner"))
{% endhighlight %}

### 실제로 사용되는 예제를 보고싶다면

아래 프로젝트들은 의존 라이브러리를 Cask로 관리하고 있습니다.

* [rejeep/emacs](https://github.com/rejeep/emacs)
* [prodigy](https://github.com/rejeep/prodigy.el)
* [emacs-jedi](https://github.com/tkf/emacs-jedi)
* [flycheck](https://github.com/lunaryorn/flycheck)
* [projectile](https://github.com/bbatsov/projectile)
* [smartparens](https://github.com/Fuco1/smartparens)
* [ecukes](https://github.com/ecukes/ecukes)
* [expand-region](https://github.com/magnars/expand-region.el)
* [and more...](https://github.com/search?l=Emacs+Lisp&q=cask&ref=opensearch&type=Code)
