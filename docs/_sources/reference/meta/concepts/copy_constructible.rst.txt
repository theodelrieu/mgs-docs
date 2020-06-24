.. _copy_constructible:

************************
meta::copy_constructible
************************

Defined in header ``<mgs/meta/concepts/copy_constructible.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept copy_constructible =
     meta::move_constructible<T> &&
     meta::constructible_from<T, T&> && meta::convertible_to<T&, T> &&
     meta::constructible_from<T, T const&> && meta::convertible_to<T const&, T> &&
     meta::constructible_from<T, T const> && meta::convertible_to<T const, T>;

Pre-C++20 implementation of the :concept:`copy_constructible` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_copy_constructible { /* ... */ };

   template <typename T>
   constexpr auto is_copy_constructible_v = is_copy_constructible<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_copy_constructible_v<T>>>
   using copy_constructible = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/copy_constructible.hpp>

   using namespace mgs::meta;

   static_assert(is_copy_constructible_v<int>, "");
   static_assert(!is_copy_constructible_v<char[]>, "");

See also
========

* :ref:`move_constructible`
* :ref:`constructible_from`
* :ref:`convertible_to`
