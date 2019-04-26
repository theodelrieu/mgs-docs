.. _regular:

*************
meta::regular
*************

Defined in header ``<mgs/meta/concepts/regular.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept regular = meta::semiregular<T> && meta::equality_comparable<T>;

Pre-C++20 implementation of the :iterconcept:`regular` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_regular { /* ... */ };

   template <typename T>
   constexpr auto is_regular_v = is_regular<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_regular_v<T>>>
   using regular = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/regular.hpp>

   using namespace mgs::meta;

   // no equality operator
   struct semiregular {};

   static_assert(is_regular_v<std::vector<int>>, "");
   static_assert(is_regular_v<int>, "");
   static_assert(!is_regular_v<semiregular>, "");

See also
========

* :ref:`semiregular`
* :ref:`equality_comparable`
