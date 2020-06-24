.. _common_range:

******************
meta::common_range
******************

Defined in header ``<mgs/meta/concepts/common_range.hpp>``.

.. code-block:: cpp

   template <typename T>
   concept common_range =
      meta::range<T> &&
      meta::same_as<meta::iterator_t<T>, meta::sentinel_t<T>>;

Pre-C++20 implementation of the :rangeconcept:`common_range` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T>
   struct is_common_range { /* ... */ };

   template <typename T>
   constexpr auto is_common_range_v = is_common_range<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_common_range_v<T>>>
   using common_range = T;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/common_range.hpp>

   using namespace mgs::meta;

   struct sentinel {};

   bool operator==(char*, pointer_sentinel);
   bool operator!=(char*, pointer_sentinel);

   bool operator==(pointer_sentinel, char*);
   bool operator!=(pointer_sentinel, char*);

   struct input_range {
     char* begin();
     sentinel end();
   };

   static_assert(is_common_range_v<std::string>, "");
   static_assert(!is_common_range_v<input_range>, "");

See also
========

* :ref:`range`
* :ref:`same_as`
* :ref:`iterator_t`
* :ref:`sentinel_t`
