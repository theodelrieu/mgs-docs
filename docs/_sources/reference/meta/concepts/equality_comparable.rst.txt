.. _equality_comparable:

*************************
meta::equality_comparable
*************************

Defined in header ``<mgs/meta/concepts/equality_comparable.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept equality_comparable = meta::weakly_equality_comparable_with<T, T>;

Pre-C++20 implementation of the :concept:`equality_comparable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_equality_comparable { /* ... */ };

   template <typename T>
   constexpr auto is_equality_comparable_v = is_equality_comparable<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_equality_comparable_v<T>>>
   using equality_comparable = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/equality_comparable.hpp>

   using namespace mgs::meta;

   static_assert(is_equality_comparable_v<std::string>, "");
   static_assert(!is_equality_comparable_v<std::mutex>, "");

See also
========

* :ref:`weakly_equality_comparable_with`
