.. _random_access_range:

*************************
meta::random_access_range
*************************

Defined in header ``<mgs/meta/concepts/random_access_range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept random_access_range =
     meta::bidirectional_range<T> && meta::random_access_iterator<meta::iterator_t<T>>;

Pre-C++20 implementation of the :rangeconcept:`random_access_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_random_access_range { /* ... */ };

   template <typename T>
   constexpr auto is_random_access_range_v = is_random_access_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_random_access_range_v<T>>>
   using random_access_range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/random_access_range.hpp>

   using namespace mgs::meta;

   static_assert(is_random_access_range_v<std::string>, "");
   static_assert(is_random_access_range_v<char [2]>, "");
   static_assert(!is_random_access_range_v<std::list<char>>, "");

See also
========

* :ref:`range`
* :ref:`random_access_iterator`
* :ref:`iterator_t`
