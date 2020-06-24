.. _semiregular:

*****************
meta::semiregular
*****************

Defined in header ``<mgs/meta/concepts/semiregular.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept semiregular = meta::copyable<T> && meta::default_constructible<T>;

Pre-C++20 implementation of the :iterconcept:`semiregular` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_semiregular { /* ... */ };

   template <typename T>
   constexpr auto is_semiregular_v = is_semiregular<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_semiregular_v<T>>>
   using semiregular = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/semiregular.hpp>

   using namespace mgs::meta;

   // no equality operator
   struct semiregular {};

   static_assert(is_semiregular_v<std::vector<int>>, "");
   static_assert(is_semiregular_v<int>, "");
   static_assert(!is_semiregular_v<semiregular>, "");

See also
========

* :ref:`copyable`
* :ref:`default_constructible`
