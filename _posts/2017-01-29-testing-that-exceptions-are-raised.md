---
title: Testing that an Exception is Raised
---

**This is part of
[a series of posts on Python unit testing]({{ site.baseurl }}{% post_url 2017-01-15-python-unit-testing %}).**

[Previously](/posts/writing-tests) we tested that the
[validate_url() function](https://github.com/hypothesis/h/blob/8d11e918005581f35f97268e9470eb3c34a6b416/h/accounts/util.py#L9)
returns the given URL if it's a valid URL. If the given URL is _not_ valid then
`validate_url()` is supposed to raise a `ValueError` exception.
To test this we need to use [pytest.raises()](http://doc.pytest.org/en/latest/getting-started.html#asserting-that-a-certain-exception-is-raised).
Here is a test that _expects_ `validate_url()` to raise a `ValueError`:

```python
def test_validate_url_rejects_urls_without_domains():
    with pytest.raises(ValueError):
        validate_url('http:///path')
```

This test will fail if the block of code inside the `with` statement _doesn't_
raise `ValueError`, otherwise the test will pass.

There's also [pytest.warns(), for testing that code raises a warning](http://docs.pytest.org/en/latest/recwarn.html)
in the same way.

In the next post we'll look at
[the arrange, act, assert recipe for writing a good test]({{ site.baseurl }}{% post_url 2017-01-29-arrange-act-assert %}).
