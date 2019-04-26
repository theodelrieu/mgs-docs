.. _dereferenceable:

*********************
meta::dereferenceable
*********************

Defined in header ``<mgs/meta/concepts/dereferenceable.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept dereferenceable = requires(T& t) {
      { *t } -> /* see below */;
    };

Pre-C++20 implementation of the *exposition-only* `dereferenceable <https://timsong-cpp.github.io/cppwp/iterator.synopsis>`__ concept.

----

The **dereferenceable** concept specifies that the type obtained when dereferencing a value of type **T** is itself referenceable.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_dereferenceable { /* ... */ };

   template <typename T>
   constexpr auto is_dereferenceable_v = is_dereferenceable<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_dereferenceable_v<T>>>
   using dereferenceable = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/dereferenceable.hpp>

   using namespace mgs::meta;

   struct invalid { void operator*(); };

   static_assert(is_dereferenceable_v<int*>, "");
   static_assert(!is_dereferenceable_v<void*>, "");
   // void cannot be referenced (i.e. void& is ill-formed)
   static_assert(!is_dereferenceable_v<invalid>, "");
