================
PKGBUILD for st
================

Patch included
==============

::

        font patch (Iosevka Term)
        color patch (Gruvbox)
        clipboard patch

How to make patch
=================

| Create `a/` and `b/` directory
| Copy file original to `a/`, file patch to `b/`
| Make a patch file

::

        diff -u a/origin b/patch > name.patch

How to check PKGBUILD
=====================

Use `namcap` ::

        makepkg -fcsi
        namcap PKGBUILD
