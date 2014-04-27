---
title: Installation
layout: default
permalink: installation.html
---

## Installation

---

To automatically install Cask, run this command:

{% highlight bash %}
$ curl -fsSkL https://raw.github.com/cask/cask/master/go | python
{% endhighlight %}

You can also clone the repository directly.

{% highlight bash %}
$ git clone https://github.com/cask/cask.git ~/.cask
{% endhighlight %}

And OSX users can install it via Homebrew:

{% highlight bash %}
$ brew install cask
{% endhighlight %}

Don't forget to add Cask's bin to your `PATH`.

{% highlight bash %}
$ export PATH="/path/to/code/cask/bin:$PATH"
{% endhighlight %}

To upgrade Cask itself and its dependencies, run:

{% highlight bash %}
$ cask upgrade-cask
{% endhighlight %}
