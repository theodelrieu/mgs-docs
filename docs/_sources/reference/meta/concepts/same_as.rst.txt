.. _same_as:

*************
meta::same_as
*************

Defined in header ``<mgs/meta/concepts/same_as.hpp>``.

.. code-block:: cpp

   template <typename T, typename U>
   concept same_as = /* see below */;

Pre-C++20 implementation of the :concept:`same_as` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename U>
   struct is_same_as { /* ... */ };

   template <typename T, typename U>
   constexpr auto is_same_as_v = is_same_as<T, U>::value;

   template <typename T, typename U,
             typename = std::enable_if_t<is_same_as_v<T, U>>>
   using same_as = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/same_as.hpp>

   using namespace mgs::meta;

   static_assert(is_same_as_v<bool, bool>, "");
   static_assert(is_same_as_v<bool, void>, "");
