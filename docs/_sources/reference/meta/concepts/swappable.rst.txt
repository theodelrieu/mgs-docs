.. _swappable:

***************
meta::swappable
***************

Defined in header ``<mgs/meta/concepts/swappable.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept swappable = requires(T& a, T& b) {
      /* using std::swap; */ swap(a, b);
   };

Pre-C++20 implementation of the :concept:`swappable` concept.

----

Differences with the C++20 version
==================================

* The implementation does not rely on :cpp:`std::ranges::swap <ranges/swap>`, but on the usual customization point idiom, i.e. ``using std::swap; swap(/* ... */);``.
* The :concept:`std::swappable_with <swappable>` concept cannot be implemented using :cpp:`std::swap <algorithm/swap>`, since it constrains its parameters to have the exact same type.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_swappable { /* ... */ };

   template <typename T>
   constexpr auto is_swappable_v = is_swappable<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_swappable_v<T>>>
   using swappable = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/swappable.hpp>

   using namespace mgs::meta;

   struct dummy_swappable {
     // prevent from being used by default std::swap 
     dummy_swappable(dummy_swappable const&) = delete;
   };

   void swap(dummy_swappable&, dummy_swappable&);

   static_assert(is_swappable_v<int>, "");
   static_assert(is_swappable_v<dummy_swappable>, "");
