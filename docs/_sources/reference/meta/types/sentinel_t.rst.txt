.. _sentinel_t:

****************
meta::sentinel_t
****************

Defined in header ``<mgs/meta/sentinel_t.hpp>``.

.. code-block:: cpp

   template <typename T>
   using sentinel_t = /* see below */;

Pre-C++20 implementation of :cpp:`std::ranges::sentinel_t <ranges/sentinel_t>`.

----

Differences with the C++20 version
==================================

* The implementation does not rely on :cpp:`std::ranges::end <ranges/end>`, but on the usual customization point idiom, i.e. ``using std::end; end(/* ... */);``.
