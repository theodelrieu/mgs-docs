.. _boolean:

*************
meta::boolean
*************

Defined in header ``<mgs/meta/concepts/boolean.hpp>``.

.. code-block:: cpp

  template <typename B>
  concept boolean =
    meta::movable<std::remove_cvref_t<B>> &&
    requires(std::remove_reference_t<B> const& b1,
             std::remove_reference_t<B> const& b2, bool const a) {
      { b1 } -> meta::convertible_to<bool>;
      { !b1 } -> meta::convertible_to<bool>;
      { b1 &&  a } -> meta::same_as<bool>;
      { b1 ||  a } -> meta::same_as<bool>;
      { b1 && b2 } -> meta::same_as<bool>;
      {  a && b2 } -> meta::same_as<bool>;
      { b1 || b2 } -> meta::same_as<bool>;
      {  a || b2 } -> meta::same_as<bool>;
      { b1 == b2 } -> meta::convertible_to<bool>;
      { b1 ==  a } -> meta::convertible_to<bool>;
      {  a == b2 } -> meta::convertible_to<bool>;
      { b1 != b2 } -> meta::convertible_to<bool>;
      { b1 !=  a } -> meta::convertible_to<bool>;
      {  a != b2 } -> meta::convertible_to<bool>;
    };

Pre-C++20 implementation of the :concept:`boolean` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_boolean { /* ... */ };

   template <typename T>
   constexpr auto is_boolean_v = is_boolean<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_boolean_v<T>>>
   using boolean = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/boolean.hpp>

   using namespace mgs::meta;

   static_assert(is_boolean_v<bool>, "");
   static_assert(is_boolean_v<std::true_type>, "");
   static_assert(!is_boolean_v<int*>, "");

See also
========

* :ref:`movable`
* :ref:`convertible_to`
