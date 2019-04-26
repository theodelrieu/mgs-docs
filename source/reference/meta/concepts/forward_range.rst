.. _forward_range:

*******************
meta::forward_range
*******************

Defined in header ``<mgs/meta/concepts/forward_range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept forward_range =
     meta::input_range<T> && meta::forward_iterator<meta::iterator_t<T>>;

Pre-C++20 implementation of the :rangeconcept:`forward_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_forward_range { /* ... */ };

   template <typename T>
   constexpr auto is_forward_range_v = is_forward_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_forward_range_v<T>>>
   using forward_range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/forward_range.hpp>

   using namespace mgs::meta;

   struct dummy_input_range {
     std::istreambuf_iterator<char> begin();
     std::istreambuf_iterator<char> end();
   };

   static_assert(is_forward_range_v<std::forward_list<char>>, "");
   static_assert(is_forward_range_v<char [2]>, "");
   static_assert(!is_forward_range_v<dummy_input_range>, "");

See also
========

* :ref:`input_range`
* :ref:`forward_iterator`
* :ref:`iterator_t`
