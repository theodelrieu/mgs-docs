.. _usage-basic:

Basic usage
===========

This section demonstrates the library's most common usage.

It is sufficient for users wanting to encode and decode data with no particular constraints.

Encoding & decoding
-------------------

Each codec exposes ``encode`` and ``decode`` functions.

Input parameters
^^^^^^^^^^^^^^^^

Codecs share a common set of contraints on ``encode``/``decode`` input parameters.
They can be one of the following:

#. a :ref:`input_range` (e.g. :cpp:`std::string <string/basic_string>`, `std::vector<unsigned char> <https://en.cppreference.com/w/cpp/container/vector>`_)
#. a pair of :ref:`input_iterator` and :ref:`sentinel_for`
#. a ``char const[]``

.. code-block:: cpp

   #include <mgs/base64.hpp>

   #include <list>
   #include <string>

   using namespace mgs;

   int main() {
     // 1. range
     std::string decoded_str("decoded text");
     std::string encoded_str("ZGVjb2RlZCB0ZXh0");
     std::list<char> encoded_list(encoded_str.begin(), encoded_str.end());
     std::list<char> decoded_list(decoded_str.begin(), decoded_str.end());

     auto encoded = base64::encode(decoded_str);
     auto decoded = base64::decode(encoded_list);
     // decltype(encoded) -> std::string
     // decltype(decoded) -> std::vector<unsigned char>

     // 2. iterator/sentinel pair
     encoded = base64::encode(decoded_list.begin(), decoded_list.end());
     decoded = base64::decode(encoded_list.begin(), encoded_list.end());

     // 3. char const[]
     encoded = base64::encode("decoded text");
   }

.. warning::

   Passing a ``char const[]`` to ``encode``/``decode`` will discard any input after the first encountered null terminator (``'\0'``).

   If you want to avoid this behavior, use the iterator/sentinel overload (2).

Return types
^^^^^^^^^^^^

Each codec defines two default return types. One for ``encode``, one for ``decode``.

Both can be overriden:

.. code-block:: cpp

   #include <mgs/base64.hpp>

   #include <list>
   #include <vector>

   using namespace mgs;

   int main() {
     auto encoded = base64::encode("decoded text");
     auto decoded = base64::decode(encoded);

     // decltype(encoded) -> std::string
     // decltype(decoded) -> std::vector<unsigned char>

     auto encoded_vec = base64::encode<std::vector<char>>("decoded text");
     auto decoded_list = base64::decode<std::list<unsigned char>>(encoded_vec);
   }

Currently all codecs use :cpp:`std::string <string/basic_string>` as the default encoded output type, and `std::vector<unsigned char> <https://en.cppreference.com/w/cpp/container/vector>`_ as the default decoded output type.

.. tip::

   You can find the list of supported return types :ref:`here <supported-return-types>`.

   If a type you wish to use is not supported by default, take a look :ref:`here <adding-support-for-user-defined-types>`.

Error handling
--------------

As of now, *mgs* reports errors with exceptions.

Every exception resides in the namespace ``mgs::errors``.

.. table::
   :align: left

   ============================================= =============================================== ===================================
   Class                                         Derived from                                    Description
   ============================================= =============================================== ===================================
   :doc:`/reference/errors/types/exception`      :cpp:`std::runtime_error <error/runtime_error>` Base class for all exceptions
   :doc:`/reference/errors/types/decode_error`   :doc:`/reference/errors/types/exception`        Base class for decoding exceptions
   :doc:`/reference/errors/types/invalid_input`  :doc:`/reference/errors/types/decode_error`     Thrown on invalid encoded input
   :doc:`/reference/errors/types/unexpected_eof` :doc:`/reference/errors/types/decode_error`     Thrown when more input was expected
   ============================================= =============================================== ===================================

.. note::

   I am well aware that using exceptions will put off users who disable them.
   I would like to support this use-case in future versions. Do not hesitate to give your feedback/ideas!

Predicting encoded/decoded size
-------------------------------

Codecs also provide two methods to predict the to-be-transformed size:

.. code-block:: cpp

   #include <mgs/base64.hpp>

   #include <cassert>

   using namespace mgs;

   int main() {
     auto const encoded_size = base64::encoded_size(42);
     auto const decoded_size = base64::max_decoded_size(encoded_size);
     assert(decoded_size == 42);

     // base64 is always padded to a multiple of 4 bytes
     auto const invalid_decoded_size = base64::max_decoded_size(3);
     assert(invalid_decoded_size == -1);
   }
