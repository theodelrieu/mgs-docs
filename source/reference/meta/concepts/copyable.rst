.. _copyable:

**************
meta::copyable
**************

Defined in header ``<mgs/meta/concepts/copyable.hpp>``.

.. code-block:: cpp

   template <typename  T>
   concept copyable =
     meta::copy_constructible<T> &&
     meta::movable<T> &&
     meta::assignable_from<T&, T const&>;

Pre-C++20 implementation of the :concept:`copyable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_copyable { /* ... */ };

   template <typename T>
   constexpr auto is_copyable_v = is_copyable<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_copyable_v<T>>>
   using copyable = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/copyable.hpp>

   using namespace mgs::meta;

   static_assert(is_copyable_v<std::string>, "");
   static_assert(!is_copyable_v<std::string&>, "");

See also
========

* :ref:`assignable_from`
* :ref:`copy_constructible`
* :ref:`movable`
