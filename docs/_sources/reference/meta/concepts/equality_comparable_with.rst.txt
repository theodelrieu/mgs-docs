.. _equality_comparable_with:

******************************
meta::equality_comparable_with
******************************

Defined in header ``<mgs/meta/concepts/equality_comparable_with.hpp>``.

.. code-block:: cpp

   template <typename T, typename U>
   concept equality_comparable_with =
     meta::equality_comparable<T> &&
     meta::equality_comparable<U> &&
     meta::common_reference_with<
       std::remove_reference_t<T> const&,
       std::remove_reference_t<U> const&> &&
     meta::equality_comparable<
       meta::common_reference_t<
         std::remove_reference_t<T> const&,
         std::remove_reference_t<U> const&>> &&
     meta::weakly_equality_comparable_with<T, U>;

Pre-C++20 implementation of the :concept:`std::equality_comparable_with <equality_comparable>` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename U>
   struct is_equality_comparable_with { /* ... */ };

   template <typename T, typename U>
   constexpr auto is_equality_comparable_with_v =
                     is_equality_comparable_with<T, U>::value;

   template <typename T, typename U,
             typename = std::enable_if_t<is_equality_comparable_v<T, U>>>
   using equality_comparable_with = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/equality_comparable_with.hpp>

   using namespace mgs::meta;

   static_assert(is_equality_comparable_with_v<int, float>, "");
   static_assert(!is_equality_comparable_with_v<std::mutex, int>, "");

See also
========

* :ref:`weakly_equality_comparable_with`
* :ref:`equality_comparable`
* :ref:`common_reference_with`
* :ref:`common_reference`
