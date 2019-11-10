---
title: Python Unit Testing
subtitle: A series of Python unit testing tutorials covering pytest, factory_boy, mock, and unit vs integrated tests.
---

This series of posts is a tutorial for an approach to unit testing in Python -
the approach used by [Hypothesis](https://hypothes.is/)'s Python web app
[h](https://github.com/hypothesis/h) (yes, the app has a single-letter name,
its code can be found at <https://github.com/hypothesis/h>) using
[tox](https://tox.readthedocs.io/),
[pytest](https://pytest.org),
[mock](http://www.voidspace.org.uk/python/mock/)
and [factory_boy](https://factoryboy.readthedocs.io/).

1. [Running the Tests]({{ site.baseurl }}{% post_url 2017-01-16-running-the-h-tests %})
1. [Debugging a Failing Test]({{ site.baseurl }}{% post_url 2017-01-28-debugging-tests %})
1. [Writing Simple Tests][]
1. [Testing that an Exception is Raised]({{ site.baseurl }}{% post_url 2017-01-29-testing-that-exceptions-are-raised %})
1. [Arrange, Act, Assert][]
1. [Factories][]
1. [Parametrize][]
1. [Fixtures][]
1. [Advanced Fixtures]({{ site.baseurl }}{% post_url 2017-02-12-advanced-fixtures %})
1. [Mock][]
1. [The Problem with Mocks]({{ site.baseurl }}{% post_url 2017-03-17-the-problem-with-mocks %})
1. [When and When Not to Use Mocks][]
1. [Sentinel][]
1. [Patch][]
1. [usefixtures as a Class Decorator][usefixtures]
1. [Matcher Objects]({{ site.baseurl }}{% post_url 2017-05-12-matchers %})

While this tutorial is based on h's approach and the examples are taken from
h's tests, most of it should be applicable to Python unit testing generally.

These posts are aimed at intermediate Python developers, not complete beginners.
Basic knowledge of [Python](https://www.python.org/) programming and
[virtualenv](https://virtualenv.pypa.io/) are assumed, for example.

In a large, real-world project like h the tests contain a lot of things that
might be unfamiliar - [factories][Factories], [parametrize][Parametrize],
[mock][Mock], [sentinel][Sentinel], [patch][Patch], [usefixtures][usefixtures]
and [test method arguments that seem to come from nowhere][Fixtures]. One of
the aims of this tutorial is to introduce you to all these, so that you can
read the Hypothesis test code and understand what's going on.

Knowing how and when to use all of these tools will help you to write better
tests. We'll also cover a few more advanced aspects of writing **good tests**,
as opposed to bad ones, particularly when we talk about
[how to organize your tests][Writing Simple Tests],
[the arrange, act, assert pattern][Arrange, Act, Assert] and test naming,
[fixtures][Fixtures], and
[how and when to use mocks][When and When Not to Use Mocks].

Finally, we'll touch even less on the important but difficult topic of how to
design **good code** that works well and is easy to test.

I also hope that these posts will serve as a reference for myself,
that I can update as my thoughts on testing evolve,
and that I can use when I start a new codebase (Python or otherwise) and want
to write good tests for it.

To get started, the first post is [Running the Tests...]({{ site.baseurl }}{% post_url 2017-01-16-running-the-h-tests %})

[Factories]: {{ site.baseurl }}{% post_url 2017-01-29-factories %}
[Parametrize]: {{ site.baseurl }}{% post_url 2017-01-31-parametrize %}
[Fixtures]: {{ site.baseurl }}{% post_url 2017-02-02-fixtures %}
[Mock]: {{ site.baseurl }}{% post_url 2017-03-17-mock %}
[Sentinel]: {{ site.baseurl }}{% post_url 2017-03-17-sentinel %}
[Patch]: {{ site.baseurl }}{% post_url 2017-03-17-patch %}
[usefixtures]: {{ site.baseurl }}{% post_url 2017-03-17-usefixtures-class-decorator %}
[Writing Simple Tests]: {{ site.baseurl }}{% post_url 2017-01-28-writing-tests %}
[Arrange, Act, Assert]: {{ site.baseurl }}{% post_url 2017-01-29-arrange-act-assert %}
[When and When Not to Use Mocks]: {{ site.baseurl }}{% post_url 2017-04-25-when-to-use-mocks %}
