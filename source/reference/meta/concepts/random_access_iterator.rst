.. _random_access_iterator:

****************************
meta::random_access_iterator
****************************

Defined in header ``<mgs/meta/concepts/random_access_iterator.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept random_access_iterator =
      meat::bidirectional_iterator<I> &&
      meat::derived_from<meta::iter_concept<I>, std::random_access_iterator_tag> &&
      meat::totally_ordered<I> &&
      meat::sized_sentinel_for<I, I> &&
      requires(I i, I const j, meta::iter_difference_t<I> const n) {
         { i += n } -> meta::same_as<I&>;
         { j +  n } -> meta::same_as<I>;
         { n +  j } -> meta::same_as<I>;
         { i -= n } -> meta::same_as<I&>;
         { j -  n } -> meta::same_as<I>;
         {   j[n] } -> meta::same_as<meta::iter_reference_t<I>>;
      };

Pre-C++20 implementation of the :concept:`random_access_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_random_access_iterator { /* ... */ };

   template <typename I>
   constexpr auto is_random_access_iterator_v = is_random_access_iterator<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_random_access_iterator_v<I>>>
   using random_access_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/random_access_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_random_access_iterator_v<std::vector<int>::iterator>, "");
   static_assert(is_random_access_iterator_v<char*>, "");
   static_assert(!is_random_access_iterator_v<std::list<char>::iterator>, "");

See also
========

* :ref:`bidirectional_iterator`
* :ref:`derived_from`
* :ref:`sized_sentinel_for`
* :ref:`totally_ordered`
* :ref:`iter_concept`
