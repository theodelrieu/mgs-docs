.. _common_reference:

**********************
meta::common_reference
**********************

Defined in header ``<mgs/meta/common_reference.hpp>``.

.. code-block:: cpp

   template <typename... T>
   struct common_reference;

   template <typename... T>
   using common_reference_t = typename common_reference<T...>::type;

Pre-C++20 implementation of :cpp:`std::common_reference <types/common_reference>`.

----

Differences with the C++20 version
==================================

* There is no ``basic_common_reference`` customization point.
