.. _iterator_traits:

*********************
meta::iterator_traits
*********************

Defined in header ``<mgs/meta/iterator_traits.hpp>``.

.. code-block:: cpp

   template <typename I>
   struct iterator_traits;

Pre-C++20 implementation of :cpp:`std::iterator_traits <iterator/iterator_traits>`.

----

This implementation is SFINAE-friendly, i.e. it fixes `LWG 2951 <https://cplusplus.github.io/LWG/issue2951>`_.
