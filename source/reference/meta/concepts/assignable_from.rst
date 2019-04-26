.. _assignable_from:

*********************
meta::assignable_from
*********************

Defined in header ``<mgs/meta/concepts/assignable_from.hpp>``.

.. code-block:: cpp

   template <typename LHS, typename RHS>
   concept assignable_from =
     std::is_lvalue_reference_v<LHS> &&
     meta::common_reference_with<
       std::remove_reference_t<LHS> const&,
       std::remove_reference_t<RHS> const&> &&
     requires(LHS lhs, RHS&& rhs) {
       lhs = std::forward<RHS>(rhs);
       requires meta::same_as<decltype(lhs = std::forward<RHS>(rhs)), LHS>;
     };

Pre-C++20 implementation of the :concept:`assignable_from` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename LHS, typename RHS>
   struct is_assignable_from { /* ... */ };

   template <typename LHS, typename RHS>
   constexpr auto is_assignable_from_v = is_assignable_from<LHS, RHS>::value;

   template <typename LHS, typename RHS,
             typename = std::enable_if_t<is_assignable_from_v<LHS, RHS>>>
   using assignable_from = LHS;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/assignable_from.hpp>

   using namespace mgs::meta;

   static_assert(is_assignable_from_v<int&, int const&>, "");
   static_assert(!is_assignable_from_v<int&, std::string>, "");

See also
========

* :ref:`common_reference_with`
* :ref:`same_as`
