---
title: Development
layout: default
permalink: development.html
---

## Development

---

The development of Cask is at Github
<https://github.com/cask/cask>. Development related discussion is done
in a Google group <https://groups.google.com/forum/#!forum/cask-dev>.

### Contribution

Be sure to!

Implement the features and don't forget to test it. To run the tests,
first start the fake ELPA server:

{% highlight bash %}
$ make start-server
{% endhighlight %}

To run the unit tests:

{% highlight bash %}
$ make unit
{% endhighlight %}

To run the integration tests:

{% highlight bash %}
$ make ecukes
{% endhighlight %}

And to run all tests:

{% highlight bash %}
$ make test
{% endhighlight %}

If all passes, send us a
[pull request](https://github.com/cask/cask/pulls) with the
changes. Note that we usually work on a WIP-branch, which is the
branch the pull request should target. They are named
`v{MAJOR}.{MINOR}-wip`. If no such branch exist, target the `master`
branch.
