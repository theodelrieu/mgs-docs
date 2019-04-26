.. _input_range:

*****************
meta::input_range
*****************

Defined in header ``<mgs/meta/concepts/input_range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept input_range =
     meta::range<T> && meta::input_iterator<meta::iterator_t<T>>;

Pre-C++20 implementation of the :rangeconcept:`input_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_input_range { /* ... */ };

   template <typename T>
   constexpr auto is_input_range_v = is_input_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_input_range_v<T>>>
   using input_range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/input_range.hpp>

   using namespace mgs::meta;

   struct output_range {
     std::back_insert_iterator<std::string> begin();
     std::back_insert_iterator<std::string> end();
   };

   static_assert(is_input_range_v<std::string>, "");
   static_assert(is_input_range_v<char [2]>, "");
   static_assert(!is_input_range_v<output_range>, "");

See also
========

* :ref:`range`
* :ref:`input_iterator`
* :ref:`iterator_t`
