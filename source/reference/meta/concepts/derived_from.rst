.. _derived_from:

******************
meta::derived_from
******************

Defined in header ``<mgs/meta/concepts/derived_from.hpp>``.

.. code-block:: cpp

   template <typename Derived, typename Base>
   concept derived_from =
      meta::complete_type<Derived> &&
      std::is_base_of_v<Base, Derived> && 
      std::is_convertible_v<Derived const volatile*, Base const volatile*>;

Pre-C++20 implementation of the :concept:`derived_from` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename Derived, typename Base>
   struct is_derived_from { /* ... */ };

   template <typename Derived, typename Base>
   constexpr auto is_derived_from_v = is_derived_from<Derived, Base>::value;

   template <typename Derived, typename Base,
             typename = std::enable_if_t<is_derived_from_v<Derived, Base>>
   using DerivedFrom = Derived;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/derived_from.hpp>

   using namespace mgs::meta;

   struct A {};
   struct B : A {};

   static_assert(is_derived_from_v<B, A>, "");
   static_assert(is_derived_from_v<A, A>, "");
   static_assert(!is_derived_from_v<A, B>, "");
