.. _move_constructible:

************************
meta::move_constructible
************************

Defined in header ``<mgs/meta/concepts/move_constructible.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept move_constructible = meta::constructible_from<T, T> && meta::convertible_to<T, T>;

Pre-C++20 implementation of the :concept:`move_constructible` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_move_constructible { /* ... */ };

   template <typename T>
   constexpr auto is_move_constructible_v = is_move_constructible<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_move_constructible_v<T>>>
   using move_constructible = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/move_constructible.hpp>

   using namespace mgs::meta;

   struct non_move_constructible {
     non_move_constructible(non_move_constructible&&) = delete;
   }

   static_assert(is_move_constructible_v<int>, "");
   static_assert(is_move_constructible_v<std::unique_ptr<int>>, "");
   static_assert(!is_move_constructible_v<non_move_constructible>, "");

See also
========

* :ref:`constructible_from`
* :ref:`convertible_to`
