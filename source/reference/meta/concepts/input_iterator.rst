.. _input_iterator:

********************
meta::input_iterator
********************

Defined in header ``<mgs/meta/concepts/input_iterator.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept input_iterator =
      meta::input_or_output_iterator<I> &&
      meta::readable<I> &&
      meta::derived_from<meta::iter_concept<I>, std::input_iterator_tag>;

Pre-C++20 implementation of the :iterconcept:`input_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_input_iterator { /* ... */ };

   template <typename I>
   constexpr auto is_input_iterator_v = is_input_iterator<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_input_iterator_v<I>>>
   using input_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/input_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_input_iterator_v<std::istreambuf_iterator<char>>, "");
   static_assert(is_input_iterator_v<char*>, "");
   // std::back_insert_iterator is an output_iterator
   static_assert(!is_input_iterator_v<std::back_insert_iterator<std::string>>, "");

See also
========

* :ref:`input_or_output_iterator`
* :ref:`readable`
* :ref:`derived_from`
* :ref:`iter_concept`
