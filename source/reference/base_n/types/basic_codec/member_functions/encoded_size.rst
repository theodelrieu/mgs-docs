*********************************
base_n::basic_codec::encoded_size
*********************************

.. code-block:: cpp

   static constexpr mgs::ssize_t encoded_size(mgs::ssize_t decoded_size);

Computes the encoded size corresponding to *decoded_size*.

----

Parameters
==========

* **decoded_size** - Decoded size, must be > 0.

Return value
============

The encoded size.

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>

   using namespace mgs;

   static_assert(base64::encoded_size(3) == 4, "");
