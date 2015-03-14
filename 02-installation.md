---
title: 설치
layout: default
permalink: installation.html
---

## 설치

---

아래 명령어를 실행하면 자동적으로 Cask가 설치됩니다.

{% highlight bash %}
$ curl -fsSkL https://raw.github.com/cask/cask/master/go | python
{% endhighlight %}

저장소를 직접 클론하는 방법도 있습니다.

{% highlight bash %}
$ git clone https://github.com/cask/cask.git ~/.cask
{% endhighlight %}

Mac OS X 사용자라면 Homebrew로 설치할 수도 있습니다.

{% highlight bash %}
$ brew install cask
{% endhighlight %}

설치가 되면 Cask를 `PATH` 환경변수에 추가하세요.

{% highlight bash %}
$ export PATH="/path/to/code/cask/bin:$PATH"
{% endhighlight %}

Cask와 Cask의 의존 라이브러리들을 업그레이드하려면 아래 명령어를 실행하세요.

{% highlight bash %}
$ cask upgrade-cask
{% endhighlight %}
