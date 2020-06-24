.. _input_or_output_iterator:

******************************
meta::input_or_output_iterator
******************************

Defined in header ``<mgs/meta/concepts/input_or_output_iterator.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept input_or_output_iterator = meta::dereferenceable<I> && meta::weakly_incrementable<I>;

Pre-C++20 implementation of the :iterconcept:`input_or_output_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_input_or_output_iterator { /* ... */ };

   template <typename I>
   constexpr auto is_input_or_output_iterator_v =
                     is_input_or_output_iterator<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_input_or_output_iterator_v<I>>>
   using input_or_output_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/input_or_output_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_input_or_output_iterator_v<std::istreambuf_iterator<char>>, "");
   static_assert(is_input_or_output_iterator_v<std::back_insert_iterator<std::string>>, "");
   static_assert(is_input_or_output_iterator_v<char*>, "");

See also
========

* :ref:`dereferenceable`
* :ref:`weakly_incrementable`
