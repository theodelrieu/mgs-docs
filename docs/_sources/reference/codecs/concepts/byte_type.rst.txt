.. _byte_type:

*****************
codecs::byte_type
*****************

Defined in header ``<mgs/codecs/concepts/byte_type.hpp>``

.. code-block:: cpp

   template <typename T>
   concept byte_type = meta::same_as<T, std::byte> ||
     (meta::integral<T> &&
     std::numeric_limits<T>::digits + std::numeric_limits<T>::is_signed ==
     std::numeric_limits<unsigned char>::digits);


The **byte_type** concept is satisfied when one of the following is true:

#. **T** is :cpp:`std::byte <types/byte>` (C++17 and beyond).
#. **T** models :ref:`integral` and can represent the same number of bits as ``unsigned char``.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T>
   struct is_byte_type
   { /* ... */ };

   template <typename T>
   constexpr auto is_byte_type_v = is_byte_type<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_byte_type_v<T>>>
   using byte_type = T;

   } // namespace codecs
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <cstddef> 
   #include <cstdint>

   #include <mgs/codecs/concepts/byte_type.hpp>

   using namespace mgs::codecs;

   static_assert(is_byte_type_v<std::byte>, "");
   static_assert(is_byte_type_v<unsigned char>, "");
   static_assert(is_byte_type_v<char>, "");

   static_assert(!is_byte_type_v<int>, "");
   static_assert(!is_byte_type_v<bool>, "");

See also
========

* :ref:`same_as`
* :ref:`integral`
