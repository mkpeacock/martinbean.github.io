---
layout: post
meta_description: I’ve re-build my website using Jekyll and share with you how.
title: Building a blog with Jekyll
---
Although I initially started writing this site in [PHP](http://php.net/), I grew bored and realised that what may seem simple and elegant in your head never ends that way when you started coding.
Therefore, I stopped and re-analysed what I wanted to do: I wanted to display posts in a template that I had created; no clutter that comes with an off-the-shelf platform like [WordPress](http://wordpress.org/).

I’d recently moved my site to [Heroku](http://heroku.com/). Because of this, I realised I was not limited to a particular stack (I’m a PHP developer by trade). Enter [Jekyll](https://github.com/mojombo/jekyll).

Jekyll is a static site generator written in [Ruby](http://www.ruby-lang.org/). I had heard good things about it from developers such as [Harry Roberts](http://csswizardry.com/) and [Jack Franklin](http://jackfranklin.co.uk/). As a keen [GitHub](http://github.com/) user, I knew GitHub Pages used Jekyll in the background too—not surprising since the author of Jekyll is a GitHub co-founder!

## Getting started

### Install Ruby
So, to get started with Jekyll we need Ruby installed on our machine. Mac OS X comes with Ruby pre-installed but if you need to install Ruby on your machine, check out the downloads page on the Ruby website: [www.ruby-lang.org/en/downloads/](http://www.ruby-lang.org/en/downloads/).

### Install gems
Next you need to install the Jekyll “gem”. A gem is package in Ruby parlance, and Jekyll is merely just a Ruby package. Install it with the following command in your command line app:

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

## Setup the directory structure

With Ruby and the Jekyll gem installed, we can then setup the directory structure required for Jekyll:

{% highlight text %}
_layouts/
    default.html
_posts/
    2013-04-24-hello-world.md
_config.yml
index.html
{% endhighlight %}

Just create blank files for the files above.

## Create a default layout

Layouts in Jekyll are just plain old HTML, with a couple of delimiters in to render the page’s title and content:

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>{% raw %}{{ page.title }}{% endraw %}</title>
  </head>
  <body>
    {% raw %}{{ content }}{% endraw %}
  </body>
</html>
{% endhighlight %}

## Listing posts

So far, nice and simple. Next step is to create your home page which will display a list of posts:

{% highlight text %}
---
layout: default
title: My Home Page
---

<h1>Latest posts</h1>
<div class="hfeed">
{% raw %}
{% for post in site.posts %}
    <article class="hentry entry">
        <h1 class="entry-title">
            <a href="{{ post.url }}" rel="bookmark">{{ post.title }}</a>
        </h1>
        <p>Posted on <span class="published">{{ post.date }}</span></p>
    </article>
{% endfor %}
{% endraw %}
</div>
{% endhighlight %}

You’ll notice at the top of **index.html** are some properties delimited by three dashes (`---`). This is what’s called [YAML Front Matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter) and is basically meta data for your page.
In the above example, we’re setting which layout to use (`default`, which will make Jekyll use <strong>_layouts/default.html</strong> to render the page) and a title for the page.

## Creating the initial post

Finally, add some content to your initial post. Open <strong>_posts/2013-04-24-hello-world.md</strong> and add the following:

{% highlight text %}
---
layout: default
title: Hello, World
---

# Hello, World

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
{% endhighlight %}

## Check the site works

So what now? Well, you should now have a basic website that can be generated by Jekyll. To test, run the following command:

{% highlight bash %}
$ jekyll serve
{% endhighlight %}

This will generate your site, and allow you to view it at [localhost:4000](http://localhost:4000). Run the command and give it a shot.

<figure>
![Hello, world](/assets/img/posts/2013-04-24-building-a-blog-with-jekyll/hello-world.png)
</figure>

## Going forward

So there you go, you now have a website powered by Jekyll! The next steps could be any of the following:

* Look at the configuration options available for use in <strong>_config.yml</strong>
* Start fleshing out the default layout
* Do the same with your home page
* Add some styling
* Add more posts
* Deploy to GitHub Pages

A good resource for getting started with Jekyll is [Jekyll Bootstrap](http://jekyllbootstrap.com/usage/jekyll-quick-start.html).
