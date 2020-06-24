.. _bidirectional_range:

*************************
meta::bidirectional_range
*************************

Defined in header ``<mgs/meta/concepts/bidirectional_range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept bidirectional_range =
     meta::forward_range<T> && meta::bidirectional_iterator<meta::iterator_t<T>>;

Pre-C++20 implementation of the :rangeconcept:`bidirectional_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_bidirectional_range { /* ... */ };

   template <typename T>
   constexpr auto is_bidirectional_range_v = is_bidirectional_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_bidirectional_range_v<T>>>
   using bidirectional_range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/bidirectional_range.hpp>

   using namespace mgs::meta;

   static_assert(is_bidirectional_range_v<std::list<char>>, "");
   static_assert(is_bidirectional_range_v<char [2]>, "");
   static_assert(!is_bidirectional_range_v<std::forward_list<char>>, "");

See also
========

* :ref:`range`
* :ref:`bidirectional_iterator`
* :ref:`iterator_t`
