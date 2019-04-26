.. _movable:

*************
meta::movable
*************

Defined in header ``<mgs/meta/concepts/movable.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept movable =
     std::is_object_v<T> &&
     meta::move_constructible<T> &&
     meta::assignable_from<T&, T> &&
     meta::swappable<T>;

Pre-C++20 implementation of the :concept:`movable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_movable { /* ... */ };

   template <typename T>
   constexpr auto is_movable_v = is_movable<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_movable_v<T>>>
   using movable = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/movable.hpp>

   using namespace mgs::meta;

   static_assert(is_movable_v<int>, "");
   static_assert(is_movable_v<std::string>, "");
   static_assert(!is_movable_v<int&>, "");

See also
========

* :ref:`move_constructible`
* :ref:`assignable_from`
* :ref:`swappable`
