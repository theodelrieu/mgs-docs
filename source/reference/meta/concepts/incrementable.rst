.. _incrementable:

*******************
meta::incrementable
*******************

Defined in header ``<mgs/meta/concepts/incrementable.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept incrementable =
      meta::regular<I> &&
      meta::weakly_incrementable<I> &&
      requires(I i) {
         { i++ } -> meta::same_as<I>;
      };

Pre-C++20 implementation of the :iterconcept:`incrementable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_incrementable { /* ... */ };

   template <typename I>
   constexpr auto is_incrementable_v = is_incrementable<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_incrementable_v<I>>>
   using incrementable = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/incrementable.hpp>

   using namespace mgs::meta;

   struct incrementable {
     using difference_type = void;
     incrementable& operator++();
     incrementable operator++(int);
   };

   struct non_incrementable {};

   static_assert(is_incrementable_v<char>, "");
   static_assert(is_incrementable_v<incrementable>, "");
   static_assert(!is_incrementable_v<non_incrementable>, "");

See also
========

* :ref:`regular`
* :ref:`weakly_incrementable`
