.. _default_constructible:

***************************
meta::default_constructible
***************************

Defined in header ``<mgs/meta/concepts/default_constructible.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept default_constructible = meta::constructible_from<T>;

Pre-C++20 implementation of the :concept:`default_constructible` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_default_constructible { /* ... */ };

   template <typename T>
   constexpr auto is_default_constructible_v = is_default_constructible<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_default_constructible_v<T>>>
   using default_constructible = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/default_constructible.hpp>

   using namespace mgs::meta;

   struct non_default_constructible {
     non_default_constructible() = delete;
   };

   static_assert(is_default_constructible_v<std::vector<int>>, "");
   static_assert(is_default_constructible_v<int>, "");
   static_assert(!is_default_constructible_v<non_default_constructible>, "");

See also
========

* :ref:`constructible_from`
