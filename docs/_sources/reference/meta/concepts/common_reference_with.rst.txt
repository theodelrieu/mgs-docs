.. _common_reference_with:

***************************
meta::common_reference_with
***************************

Defined in header ``<mgs/meta/concepts/common_reference_with.hpp>``.

.. code-block:: cpp

   template <typename T, typename U>
   concept common_reference_with =
      meta::same_as<meta::common_reference_t<T, U>, meta::common_reference_t<U, T>> &&
      meta::convertible_to<T, meta::common_reference_t<T, U>> &&
      meta::convertible_to<U, meta::common_reference_t<T, U>>;

Pre-C++20 implementation of the :concept:`common_reference_with` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename U>
   struct has_common_reference_with { /* ... */ };

   template <typename T, typename U>
   constexpr auto has_common_reference_with_v = has_common_reference_with<T, U>::value;

   template <typename T, typename U,
             typename = std::enable_if_t<has_common_reference_with_v<T, U>>>
   using common_reference_with = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/common_reference_with.hpp>

   using namespace mgs::meta;

   static_assert(has_common_reference_with_v<int&, short&>, "");
   static_assert(has_common_reference_with_v<int const&, int volatile&>, "");
   static_assert(!has_common_reference_with_v<int, char (&)[]>, "");

See also
========

* :ref:`convertible_to`
* :ref:`common_reference`
