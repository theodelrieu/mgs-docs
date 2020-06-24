.. _output_iterator:

*********************
meta::output_iterator
*********************

Defined in header ``<mgs/meta/concepts/output_iterator.hpp>``.

.. code-block:: cpp

   template <typename I, typename T>
   concept output_iterator =
      meta::input_or_output_iterator<I> &&
      meta::writable<I, T> &&
      requires(I i, T&& t) {
         *i++ = std::forward<T>(t);
      };

Pre-C++20 implementation of the :iterconcept:`output_iterator` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I, typename T>
   struct is_output_iterator { /* ... */ };

   template <typename I, typename T>
   constexpr auto is_output_iterator_v = is_output_iterator<I, T>::value;

   template <typename I, typename T,
             typename = std::enable_if_t<is_output_iterator_v<I, T>>>
   using output_iterator = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/output_iterator.hpp>

   using namespace mgs::meta;

   static_assert(is_output_iterator_v<std::back_insert_iterator<std::string>>, "");
   static_assert(is_output_iterator_v<char*>, "");

   static_assert(!is_output_iterator_v<char const*>, "");
   static_assert(!is_output_iterator_v<std::istreambuf_iterator<char>>, "");

See also
========

* :ref:`input_or_output_iterator`
* :ref:`writable`
