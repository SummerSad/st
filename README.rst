================
PKGBUILD for st
================

Patch included
==============

::

        theme.patch (Iosevka Term and Gruvbox)
        clipboard patch
        scrollback with mouse patch

How to make patch
=================

| Create `a/` and `b/` directory
| Copy file original to `a/`, file patch to `b/`

Make a patch file ::

        diff -u a/origin b/patch > name.patch

How to check PKGBUILD
=====================

Use `namcap` ::

        makepkg -fcsi
        namcap PKGBUILD
