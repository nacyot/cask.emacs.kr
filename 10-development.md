---
title: 개발
layout: default
permalink: development.html
---

## 개발(Development)

---

Cask 개발은 Github에서 관리되고 있습니다. 개발과 관련된 논의는 구글 그룹 <https://groups.google.com/forum/#!forum/cask-dev>을 통해서 이루어집니다.

### 기여하기

잊지마세요!

새로운 기능을 추가할 때는 반드시 테스트도 추가해주시기 바랍니다. 테스트를 실행하기 위해서 가짜 ELPA 서버를 실행합니다.

{% highlight bash %}
$ make start-server
{% endhighlight %}

단위 테스트를 실행합니다.

{% highlight bash %}
$ make unit
{% endhighlight %}

통합 테스트를 실행합니다.

{% highlight bash %}
$ make ecukes
{% endhighlight %}

다음으로 모든 테스트를 실행합니다.

{% highlight bash %}
$ make test
{% endhighlight %}

모든 테스트가 통과되면 변경사항을 [풀리퀘스트](https://github.com/cask/cask/pulls)로 보내주세요. 개발은 주로 WIP 브랜치에서 진행되고 있으며 풀리퀘스트는 이 브랜치로 보내주셔야합니다. 브랜치 이름은 `v{MAJOR}.{MINOR}-wip` 형식을 따릅니다. 만약 해당하는 브랜치가 없으면 `master` 브랜치로 풀리퀘스트를 보내주세요.
