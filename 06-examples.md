---
title: Examples
layout: default
permalink: examples.html
---

## Examples

---

Here are a few examples of how a `Cask`-file might look like.

### Emacs configuration

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

### package development

{% highlight cl %}
(source melpa)

(package-file "super.el")

(files "super.el" "bin")

(development
 (depends-on "el-mock")
 (depends-on "ecukes")
 (depends-on "ert-runner"))
{% endhighlight %}

### I still don't get it, give me some real examples

These are some projects and configurations using Cask:

* [rejeep/emacs](https://github.com/rejeep/emacs)
* [prodigy](https://github.com/rejeep/prodigy.el)
* [emacs-jedi](https://github.com/tkf/emacs-jedi)
* [flycheck](https://github.com/lunaryorn/flycheck)
* [projectile](https://github.com/bbatsov/projectile)
* [smartparens](https://github.com/Fuco1/smartparens)
* [ecukes](https://github.com/ecukes/ecukes)
* [expand-region](https://github.com/magnars/expand-region.el)
* [and more...](https://github.com/search?l=Emacs+Lisp&q=cask&ref=opensearch&type=Code)
