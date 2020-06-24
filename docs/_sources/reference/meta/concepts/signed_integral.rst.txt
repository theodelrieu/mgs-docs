.. _signed_integral:

*********************
meta::signed_integral
*********************

Defined in header ``<mgs/meta/concepts/signed_integral.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept signed_integral = meta::integral<T> && std::is_signed<T>::value;

Pre-C++20 implementation of the :concept:`signed_integral` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_signed_integral { /* ... */ };

   template <typename T>
   constexpr auto is_signed_integral_v = is_signed_integral<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_signed_integral_v<T>>>
   using signed_integral = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/signed_integral.hpp>

   using namespace mgs::meta;

   static_assert(is_signed_integral_v<int>, "");
   static_assert(!is_signed_integral_v<unsigned int>, "");
