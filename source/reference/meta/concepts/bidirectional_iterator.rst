.. _bidirectional_iterator:

****************************
meta::bidirectional_iterator
****************************

Defined in header ``<mgs/meta/concepts/bidirectional_iterator.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept bidirectional_iterator =
     meta::forward_iterator<I> &&
     meta::derived_from<meta::iter_concept<I>, std::bidirectional_iterator_tag> &&
     requires(I i) {
       { --i } -> meta::same_as<I&>;
       { i-- } -> meta::same_as<I>;
     };

Pre-C++20 implementation of the :concept:`bidirectional_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_bidirectional_iterator { /* ... */ };

   template <typename I>
   constexpr auto is_bidirectional_iterator_v = is_bidirectional_iterator<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_bidirectional_iterator_v<I>>>
   using bidirectional_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/bidirectional_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_bidirectional_iterator_v<std::list<int>::iterator>, "");
   static_assert(is_bidirectional_iterator_v<char*>, "");
   static_assert(!is_bidirectional_iterator_v<std::istreambuf_iterator<char>>, "");

See also
========

* :ref:`forward_iterator`
* :ref:`derived_from`
* :ref:`iter_concept`
