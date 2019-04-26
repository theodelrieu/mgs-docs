.. _weakly_incrementable:

**************************
meta::weakly_incrementable
**************************

Defined in header ``<mgs/meta/concepts/weakly_incrementable.hpp>``.

.. code-block:: cpp

   template <typename I>
   concept weakly_incrementable =
     meta::semiregular<I> &&
     requires(I i) {
       typename meta::iter_difference_t<I>;
       requires meta::signed_integral<meta::iter_difference_t<I>>;
       { ++i } -> meta::same_as<I&>;
       i++;
     };

Pre-C++20 implementation of the :iterconcept:`weakly_incrementable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename I>
   struct is_weakly_incrementable { /* ... */ };

   template <typename I>
   constexpr auto is_weakly_incrementable_v = is_weakly_incrementable<I>::value;

   template <typename I,
             typename = std::enable_if_t<is_weakly_incrementable_v<I>>>
   using weakly_incrementable = I;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/weakly_incrementable.hpp>

   using namespace mgs::meta;

   struct dummy_weakly_incrementable {
     using difference_type = std::ptrdiff_t;

     dummy_weakly_incrementable& operator++();
     dummy_weakly_incrementable operator++(int);
   };

   static_assert(is_weakly_incrementable_v<int>, "");
   static_assert(is_weakly_incrementable_v<dummy_weakly_incrementable>, "");

See also
========

* :ref:`signed_integral`
* :ref:`semiregular`
* :ref:`same_as`
* :ref:`iter_difference_t`
