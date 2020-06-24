.. _integral:

**************
meta::integral
**************

Defined in header ``<mgs/meta/concepts/integral.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept integral = std::is_integral<T>::value;

Pre-C++20 implementation of the :concept:`integral` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_integral { /* ... */ };

   template <typename T>
   constexpr auto is_integral_v = is_integral<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_integral_v<T>>>
   using integral = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/integral.hpp>

   using namespace mgs::meta;

   static_assert(is_integral_v<int>, "");
   static_assert(!is_integral_v<float>, "");
