---
draft: true
sitemap: false
robots: noindex, nofollow
tag: Python
---

Distinguishing Public from Internal Interfaces in Python
========================================================

My take on how to distinguish public from internal interfaces in Python,
by using `__all__` and leading _underscores. For small and quick projects I
wouldn't bother with `__all__`, and would just use leading underscores. For bigger
projects I use both `__all__` and leading underscores together as PEP 8 tells
you to. Details:

TLDR
----

You should distinguish your public and internal interfaces by using both
`__all__` and names with leading underscores:

1. You should list every module's public names in an `__all__` tuple (of
   strings) at the top of the file.

   The `__all__` in an `__init__.py` file lists the _package's_ public names.

   A module with no public interface should have an empty `__all__`:
   `__all__ = (,)`.

   You can make a name with a leading underscore, or an imported name, part of
   your public interface by adding it to `__all__` (both types of name would
   otherwise be considered internal by default).
   
   You can also make a name that _doesn't_ have a leading underscore
   (and would be considered public by default without an `__all__`)
   internal by having an `__all__` and omitting the name from it.

2. You should make every internal name start with a leading underscore.

   This applies to packages, modules, classes, functions, attributes and other
   names, and should be done in addition to `__all__`.

   Since only modules can have an `__all__`, leading underscores are the only
   way to [distinguish internal names in classes](https://docs.python.org/3/tutorial/classes.html#tut-private)
   (e.g. private methods).

`__all__` and the leading underscore complement each other:

* `__all__` provides the explicit single source of truth, and also provides a
  summary list of all the public names in one place at the top of the file.
* Leading underscores provide hints to the reader throughout
  the code, without always having to go up to the top of the file to check the
  `__all__`. And they're the only way to distinguish internal interfaces in a
  class.

`__all__` overrides the leading underscore when the two disagree:

* If a name with a leading underscore is in the `__all__`, then it's public
* If a name _without_ a leading underscore is _not_ in the `__all__`, then it's
  internal

PEP 8 contains a [Public and Internal Interfaces](https://www.python.org/dev/peps/pep-0008/#public-and-internal-interfaces) section that documents much of this.

`__all__`
---------

Modules should use `__all__` to explicitly declare their public names in order to support introspection. From PEP 8:

> To better support introspection, modules should explicitly declare the names in their public API using the `__all__` attribute. Setting `__all__` to an empty list indicates that the module has no public API.

Of course the `__all__` also acts as documentation for any programmer reading the code.

`__all__` only works with modules (and packages via their `__init__.py` modules).
You can't use `__all__` to declare the public interface of a class.

`__all__` can also be used to explicitly add an imported name or a name that begins with a leading underscore, to a module's public interface (both types of name would otherwise be considered internal by default).

`__all__` is also [used by `import *` statements](https://docs.python.org/3/tutorial/modules.html?highlight=__all__#importing-from-a-package).

Leading underscores
-------------------

In addition to docstrings and `__all__`, leading underscores should be used for internal packages, modules, classes, functions, and other names. From PEP 8:

> Even with `__all__` set appropriately, internal interfaces (packages, modules, classes, functions, attributes or other names) should still be prefixed with a single leading underscore

A leading underscore is referred to elsewhere in PEP 8 as a _weak "internal use" indicator._ There are sometimes edge cases where you want to use `__all__` to explicitly make a name with a leading underscore part of a public interface, for example:

* To avoid name conflicts.

  The standard library's [`namedtuple`'s](https://docs.python.org/3/library/collections.html#collections.namedtuple) have public names that begin with leading underscores: `_asdict()`, `_replace()`, `_fields` and `_field_defaults`. These _are_ intended to be used by external code (they're documented as such). They're presumaby named with leading underscores to avoid conflicts with user-chosen names, otherwise you wouldn't be able to use `"replace"` as a field name in a `namedtuple` class, for example.

* If a name was originally intended to be internal but it got used by external code anyway, so now you're making it officially part of the public interface, but you don't want to rename it (you don't want to remove the leading underscore) as that would break the external code that's already using it.

Imported names are internal by default
--------------------------------------

PEP 8 again:

> Imported names should always be considered an implementation detail ... unless they are an explicitly documented part of the containing module's API, such as `os.path` or a package's `__init__` module that exposes functionality from submodules.

So you don't need to worry about imported names without leading underscores becoming part of your module's public interface.

If you _do_ want to make an imported name part of your module's public interface you can add it to the module's `__all__`.

The "package's `__init__` module that exposes functionality from submodules" pattern that PEP 8 refers to is this common pattern in Python:

```python
# mypackage/__init__.py

from mypackage._foo import Foo
from mypackage._bar import Bar

__all__ = ("Foo", "Bar")
```

`mypackage/__init__.py` imports the `Foo` and `Bar` classes from the internal `_foo.py` and `_bar.py` modules and explicitly adds them to the package's public interface (its `__all__`).

External code is expected to do `import mypackage` and use `mypackage.Foo`, or do `from mypackage import Foo`. Rather than importing the internal `_foo` module. The fact that the code implementing `Foo` and `Bar` is organised into `_foo.py` and `_bar.py` is an internal detail of `mypackage` that external code shouldn't depend on. `mypackage` can be reorganised internally without breaking its public interface.

This allows you to do things like break up the `_foo.py` module into multiple smaller modules if it's getting too large,
without changing your package's public interface.

Contents of internal namespaces are automatically internal as well
------------------------------------------------------------------

PEP 8:

> An interface is also considered internal if any containing namespace (package, module or class) is considered internal.

So for example if you have a `_foo.py` module, which is internal because it has a leading underscore, you _don't_ need to also add a leading underscore to every name inside `_foo.py`. Those are already considered internal because `_foo.py` is internal.

Documentation
-------------

Finally, your documentation has the last say. If your docs (docstrings or otherwise) say that a name is public, then it's public, even if it has a leading underscore and is missing from the `__all__`. And if you _haven't_ documented an interface then it should be considered internal no matter what. PEP 8:

> Documented interfaces are considered public, unless the documentation explicitly declares them to be provisional or internal interfaces exempt from the usual backwards compatibility guarantees. All undocumented interfaces should be assumed to be internal.
