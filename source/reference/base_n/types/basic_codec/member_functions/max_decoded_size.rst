*************************************
base_n::basic_codec::max_decoded_size
*************************************

.. code-block:: cpp

   static constexpr mgs::ssize_t max_decoded_size(mgs::ssize_t encoded_size);

Computes the maximum decoded size corresponding to *encoded_size*.

----

Parameters
==========

* **encoded_size** - Encoded size, must be > 0.

Return value
============

The maximum decoded size, or ``-1`` if **encoded_size** does not represent a valid encoded size.

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>

   using namespace mgs;

   static_assert(base64::max_decoded_size(4) == 3, "");
   static_assert(base64::max_decoded_size(3) == -1, "");
