.. _destructible:

******************
meta::destructible
******************

Defined in header ``<mgs/meta/concepts/destructible.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept destructible = std::is_nothrow_destructible_v<T>;

Pre-C++20 implementation of the :concept:`destructible` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_destructible { /* ... */ };

   template <typename T>
   constexpr auto is_destructible_v = is_destructible<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_destructible_v<T>>>
   using destructible = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/destructible.hpp>

   using namespace mgs::meta;

   namespace {
   struct A {
     ~A() noexcept(false) {};
   };
   }

   static_assert(is_destructible_v<int>, "");
   static_assert(!is_destructible_v<A>, "");
