************
Introduction
************

What is a codec?
================

From Wikipedia:

.. code-block:: text

   A codec is a [...] computer program for encoding or decoding a digital data stream [...].

   Codec is a portmanteau of coder-decoder. 

Some famous codecs are: ``base64``, ``FLAC``, ``zip``.

Why should I use *mgs*?
=======================

*mgs* defines a common interface for all supported codecs, that is both generic and customizable.

.. code-block:: cpp

   #include <mgs/base64.hpp>

   #include <array>
   #include <forward_list>
   #include <string>
   #include <vector>

   using namespace mgs;

   int main() {
     std::string const a = base64::encode("Hello, World!");
     std::vector<unsigned char> const b = base64::decode(a);

     // Default return types can be overriden
     auto const c = base64::encode<std::forward_list<char>>(b);
     auto const d = base64::decode<std::array<char, 13>>(c);

     // Iterator ranges are supported
     auto const e = base64::encode(d.begin(), d.end());
     auto const f = base64::decode(e.begin(), e.end());
   }


This should cover most people's needs.
More advanced use-cases are discussed in later sections.

Scope
=====

The goal of this library is to be a collection of codecs.

Here is the list of currently supported codecs:

* :doc:`/reference/base64`
* :doc:`base64url </reference/base64url>`
* :doc:`/reference/base32`
* :doc:`/reference/base32hex`
* :doc:`/reference/base16`

Requirements
============

*mgs* is header-only, and only requires a C++14 compiler.

Documentation-wise, basic knowledge of :cpp:`concepts <language/constraints>` is recommended.

Although they are not yet available and thus not used in the code, the documentation relies on them. Consider taking a look :doc:`here </concepts_refresher>` to have a quick introduction.

Credits
=======

This library is heavily inspired from `cppcodec`_.

I first wanted to contribute to `cppcodec`_ by lifting some API constraints (i.e. being able to decode ``std::array``).

However, it was harder than it seemed so I started a side-project from scratch to experiment on API genericity and user-defined type conversions.

It ended up as a complete rewrite...

.. _cppcodec: https://github.com/tplgy/cppcodec
