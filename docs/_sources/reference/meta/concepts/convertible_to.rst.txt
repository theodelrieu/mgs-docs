.. _convertible_to:

********************
meta::convertible_to
********************

Defined in header ``<mgs/meta/concepts/convertible_to.hpp>``.

.. code-block:: cpp

   template <typename From, typename To>
   concept convertible_to =
     std::is_convertible_v<From, To> &&
     requires(From (&f)()) {
       static_cast<To>(f());
     };

Pre-C++20 implementation of the :concept:`convertible_to` concept.

----

Differences with the C++20 version
==================================

* Checks template arguments before calling :cpp:`std::is_convertible_v <types/is_convertible>`, which is not SFINAE-friendly.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename From, typename To>
   struct is_convertible_to { /* ... */ };

   template <typename From, typename To>
   constexpr auto is_convertible_to_v = is_convertible_to<From, To>::value;

   template <typename From, typename To,
             typename = std::enable_if_t<is_convertible_to_v<From, To>>
   using convertible_to = From;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/convertible_to.hpp>

   using namespace mgs::meta;

   struct A {};
   struct B { explicit operator A(); };
   struct C { operator A(); };

   static_assert(is_convertible_to_v<C, A>, "");
   static_assert(!is_convertible_to_v<B, A>, "");
