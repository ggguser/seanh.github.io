---
tags: [Hypothesis, Python Unit Tests at Hypothesis]
redirect_from:
  - /post/python-unit-testing/
---

Python Unit Tests at Hypothesis
===============================

This is the index page for a series of posts about our approach to Python unit
tests at [Hypothesis](https://hypothes.is/):

<ol>
  {% for post in site.tags["Python Unit Tests at Hypothesis"] reversed %}
    {% if post == page %}{% continue %}{% endif %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ol>

While this tutorial is based on Hypothesis's approach and the examples are
taken from Hypothesis's tests, most of it should be applicable to Python unit
testing generally.

These posts are aimed at intermediate Python developers, not complete beginners.
Basic knowledge of [Python](https://www.python.org/) programming and
[virtualenv](https://virtualenv.pypa.io/) are assumed, for example.

In a large, real-world project like Hypothesis the tests contain a lot of
things that might be unfamiliar - factories, `parametrize`, mocks, `sentinel`,
`patch`, `usefixtures` and [test method arguments that seem to come from nowhere](./python-unit-tests-at-hypothesis/_posts/2017-02-02-fixtures.md).
One of the aims of this tutorial is to introduce you to all these, so that you
can read the Hypothesis test code and understand what's going on.

Knowing how and when to use all of these tools will help you to write better
tests. We'll also cover a few more advanced aspects of writing **good tests**,
as opposed to bad ones, particularly when we talk about how to organize your
tests; the arrange, act, assert pattern and test naming; fixtures; and how and
when to use mocks.

Finally, we'll touch even less on the important but difficult topic of how to
design **good code** that works well and is easy to test.
