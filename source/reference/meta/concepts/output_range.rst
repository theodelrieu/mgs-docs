.. _output_range:

******************
meta::output_range
******************

Defined in header ``<mgs/meta/concepts/output_range.hpp>``.

.. code-block:: cpp

   template <typename R, typename T>
   concept output_range =
     meta::range<R> && meta::output_iterator<meta::iterator_t<R>, T>;

Pre-C++20 implementation of the :rangeconcept:`output_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename R, typename T>
   struct is_output_range { /* ... */ };

   template <typename R, typename T>
   constexpr auto is_output_range_v = is_output_range<R, T>::value;

   template <typename R,
             typename T,
             typename = std::enable_if_t<is_output_range_v<R, T>>>
   using output_range = R;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/output_range.hpp>

   using namespace mgs::meta;

   struct input_range {
     char const* begin();
     char const* end();
   };

   static_assert(is_output_range_v<std::string, char>, "");
   static_assert(is_output_range_v<char [2], char>, "");
   static_assert(!is_output_range_v<input_range, char>, "");

See also
========

* :ref:`range`
* :ref:`output_iterator`
* :ref:`iterator_t`
