.. _weakly_equality_comparable_with:

*************************************
meta::weakly_equality_comparable_with
*************************************

Defined in header ``<mgs/meta/concepts/weakly_equality_comparable_with.hpp>``.

.. code-block:: cpp

   template <typename T, typename U>
   concept weakly_equality_comparable_with =
     requires(std::remove_reference_t<T> const& t,
              std::remove_reference_t<U> const& u) {
       { t == u } -> meta::boolean;
       { t != u } -> meta::boolean;
       { u == t } -> meta::boolean;
       { u != t } -> meta::boolean;
     };

Pre-C++20 implementation of the *exposition-only* `weakly-equality-comparable-with <https://timsong-cpp.github.io/cppwp/concepts.compare#concept.equalitycomparable>`__ concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename U>
   struct is_weakly_equality_comparable_with { /* ... */ };

   template <typename T, typename U>
   constexpr auto is_weakly_equality_comparable_with_v =
                     is_weakly_equality_comparable_with<T, U>::value;

   template <typename T, typename U,
             typename = std::enable_if_t<is_weakly_equality_comparable_v<T, U>>>
   using weakly_equality_comparable_with = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/weakly_equality_comparable_with.hpp>

   struct A {};
   struct B {};

   bool operator==(A, A);
   bool operator!=(A, A);

   bool operator==(B, B);
   bool operator!=(B, B);

   bool operator==(A, B);
   bool operator==(B, A);

   bool operator!=(A, B);
   bool operator!=(B, A);

   static_assert(is_weakly_equality_comparable_with_v<int, float>, "");
   static_assert(is_weakly_equality_comparable_with_v<A, B>, "");
   static_assert(!is_equality_comparable_with_v<A, B>, "");

See also
========

* :ref:`boolean`
