.. _forward_iterator:

**********************
meta::forward_iterator
**********************

Defined in header ``<mgs/meta/concepts/forward_iterator.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept forward_iterator =
      meta::input_iterator<I> &&
      meta::derived_from<meta::iter_concept<I>, std::forward_iterator_tag> &&
      meta::incrementable<I> &&
      meta::sentinel_for<I, I>;

Pre-C++20 implementation of the :iterconcept:`forward_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_forward_iterator { /* ... */ };

   template <typename I>
   constexpr auto is_forward_iterator_v = is_forward_iterator<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_forward_iterator_v<I>>>
   using forward_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/forward_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_forward_iterator_v<std::forward_list<int>::iterator>, "");
   static_assert(is_forward_iterator_v<char*>, "");
   static_assert(!is_forward_iterator_v<std::istreambuf_iterator<char>>, "");

See also
========

* :ref:`input_iterator`
* :ref:`derived_from`
* :ref:`iter_concept`
