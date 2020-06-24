.. _sized_sentinel_for:

************************
meta::sized_sentinel_for
************************

Defined in header ``<mgs/meta/concepts/sized_sentinel_for.hpp>``.

.. code-block:: cpp

   template <typename S, typename I>
   concept sized_sentinel_for =
     meta::sentinel_for<S, I> &&
     requires(I const& i, S const& s) {
       { s - i } -> meta::same_as<meta::iter_difference_t<I>>;
       { i - s } -> meta::same_as<meta::iter_difference_t<I>>;
     }
   };

Pre-C++20 implementation of the :iterconcept:`sized_sentinel_for` concept.

----

Differences with the C++20 version
==================================

* There is no ``disable_sized_sentinel`` customization point.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename S, typename I>
   struct is_sized_sentinel { /* ... */ };

   template <typename S, typename I>
   constexpr auto is_sized_sentinel_v = is_sized_sentinel<S, I>::value;

   template <typename S, typename I,
             typename = std::enable_if_t<is_sized_sentinel_v<S, I>>>
   using sized_sentinel_for = S;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/sized_sentinel_for.hpp>

   using namespace mgs::meta;

   static_assert(is_sized_sentinel_for_v<char*, char*>, "");
   static_assert(is_sized_sentinel_for_v<std::vector<int>::iterator, std::vector<int>::iterator>, "");
   static_assert(!is_sized_sentinel_for_v<std::list<int>::iterator, std::list<int>::iterator>, "");

See also
========

* :ref:`sentinel_for`
* :ref:`iter_difference_t`
