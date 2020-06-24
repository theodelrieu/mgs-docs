.. _iterator_t:

****************
meta::iterator_t
****************

Defined in header ``<mgs/meta/iterator_t.hpp>``.

.. code-block:: cpp

   template <typename T>
   using iterator_t = /* see below */;

Pre-C++20 implementation of :cpp:`std::ranges::iterator_t <ranges/iterator_t>`.

----

Differences with the C++20 version
==================================

* The implementation does not rely on :cpp:`std::ranges::begin <ranges/begin>`, but on the usual customization point idiom, i.e. ``using std::begin; begin(/* ... */);``.
