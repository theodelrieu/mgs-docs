.. _totally_ordered_with:

**************************
meta::totally_ordered_with
**************************

Defined in header ``<mgs/meta/concepts/totally_ordered_with.hpp>``.

.. code-block:: cpp

   template <typename T, typename U>
   concept totally_ordered_with =
     meta::totally_ordered<T> &&
     meta::totally_ordered<U> &&
     meta::common_reference_with<
       std::remove_reference_t<T> const&,
       std::remove_reference_t<U> const&> &&
     meta::totally_ordered<
       meta::common_reference_t<
         std::remove_reference_t<T> const&,
         std::remove_reference_t<U> const&>> &&
     meta::equality_comparable_with<T, U> &&
     requires(std::remove_reference_t<T> const& t,
              std::remove_reference_t<U> const& u) {
       { t <  u } -> meta::boolean;
       { t >  u } -> meta::boolean;
       { t <= u } -> meta::boolean;
       { t >= u } -> meta::boolean;
       { u <  t } -> meta::boolean;
       { u >  t } -> meta::boolean;
       { u <= t } -> meta::boolean;
       { u >= t } -> meta::boolean;
     };

Pre-C++20 implementation of the :concept:`std::totally_ordered_with <totally_ordered>` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename U>
   struct is_totally_ordered_with { /* ... */ };

   template <typename T, typename U>
   constexpr auto is_totally_ordered_with_v =
                     is_totally_ordered_with<T, U>::value;

   template <typename T, typename U,
             typename = std::enable_if_t<is_totally_ordered_with_v<T, U>>>
   using totally_ordered_with = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/totally_ordered_with.hpp>

   using namespace mgs::meta;

   static_assert(is_totally_ordered_with_v<int, float>, "");
   static_assert(!is_totally_ordered_with_v<int, std::vector<int>>, "");

See also
========

* :ref:`totally_ordered`
* :ref:`common_reference_with`
* :ref:`boolean`
* :ref:`equality_comparable_with`
* :ref:`common_reference`
