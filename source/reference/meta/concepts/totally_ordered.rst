.. _totally_ordered:

*********************
meta::totally_ordered
*********************

Defined in header ``<mgs/meta/concepts/totally_ordered.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept totally_ordered =
     meta::equality_comparable<T> &&
     requires(std::remove_reference_t<T> const& a,
              std::remove_reference_t<T> const& b) {
     { a <  b } -> meta::boolean;
     { a >  b } -> meta::boolean;
     { a <= b } -> meta::boolean;
     { a >= b } -> meta::boolean;
   };

Pre-C++20 implementation of the :concept:`totally_ordered` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_totally_ordered { /* ... */ };

   template <typename T>
   constexpr auto is_totally_ordered_v =
                     is_totally_ordered<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_totally_ordered_v<T>>>
   using totally_ordered = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/totally_ordered.hpp>

   using namespace mgs::meta;

   struct ordered {};

   bool operator==(ordered const&, ordered const&);
   bool operator!=(ordered const&, ordered const&);
   bool operator<(ordered const&, ordered const&);
   bool operator>(ordered const&, ordered const&);
   bool operator<=(ordered const&, ordered const&);
   bool operator>=(ordered const&, ordered const&);

   static_assert(is_totally_ordered_v<int>, "");
   static_assert(is_totally_ordered_v<ordered>, "");

See also
========

* :ref:`boolean`
* :ref:`equality_comparable`
