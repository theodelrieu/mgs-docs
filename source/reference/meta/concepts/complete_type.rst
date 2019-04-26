.. _complete_type:

*******************
meta::complete_type
*******************

Defined in header ``<mgs/meta/concepts/complete_type.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept complete_type = requires {
     sizeof(T);
   };

The **CompleteType** concept is satisfied when **T** is a complete type.

.. note::

   This concept is not part of C++20.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_complete_type { /* ... */ };

   template <typename T>
   constexpr auto is_complete_type_v = is_complete_type<T>::value;

   template <typename T
             typename = std::enable_if_t<is_complete_type_v<T>>>
   using complete_type = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/complete_type.hpp>

   using namespace mgs::meta;

   static_assert(is_complete_type_v<void*>, "");
   static_assert(!is_complete_type_v<void>, "");
