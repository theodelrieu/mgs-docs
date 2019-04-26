.. _range:

***********
meta::range
***********

Defined in header ``<mgs/meta/concepts/range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept range = 
     requires(T&& t) {
       /* using std::begin; */ begin(t);
       /* using std::end; */ end(t);
     };

Pre-C++20 implementation of the :rangeconcept:`range` concept.

----

Differences with the C++20 version
==================================

* The implementation does not rely on :cpp:`std::ranges::begin <ranges/begin>`, but on the usual customization point idiom, i.e. ``using std::begin; begin(/* ... */);``.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_range { /* ... */ };

   template <typename T>
   constexpr auto is_range_v = is_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_range_v<T>>>
   using range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/range.hpp>

   using namespace mgs::meta;

   struct output_range {
     std::back_insert_iterator<std::string> begin();
     std::back_insert_iterator<std::string> end();
   };

   static_assert(is_range_v<std::string>, "");
   static_assert(is_range_v<char [2]>, "");
   static_assert(is_range_v<output_range>, "");
