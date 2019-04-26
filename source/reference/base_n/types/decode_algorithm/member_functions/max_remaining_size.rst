********************************************
base_n::decode_algorithm::max_remaining_size
********************************************

.. code-block:: cpp

   mgs::ssize_t max_remaining_size() const;

Computes the maximum number of remaining bytes.

----

Constraints
===========

This function is only defined if **IS** models :ref:`sized_input_source`.

Parameters
==========

None.

Return value
============

The maximum number of remaining bytes.

Example
=======

.. code-block:: cpp

   #include <iostream>
   #include <string>

   #include <mgs/base_n/decode_algorithm.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;
   using namespace mgs::base_n;

   namespace {

   struct base2_encoding_traits {
     // using C++17 inline variables for simplicity
     inline static char const alphabet[] = {'0', '1'};
     inline static auto const padding_policy = base_n::padding_policy::none;

     static int index_of(char c) {
       if (c == '0') return 0;
       if (c == '1') return 1;
       return -1;
     }
   };
   }  // namespace

   int main() {
     using input_source_t =
         codecs::iterator_sentinel_source<std::string::iterator>;
     using base2_decode = decode_algorithm<base2_encoding_traits, input_source_t>;

     std::string hello(
         "01001000"
         "01100101"
         "01101100"
         "01101100"
         "01101111"
         "00101100"
         "00100000"
         "01010111"
         "01101111"
         "01110010"
         "01101100"
         "01100100"
         "00100001");
     auto input_source = codecs::make_iterator_sentinel_source(hello);

     base2_decode algo(input_source);
     std::cout << "Maximum remaining decoded size: " << algo.max_remaining_size()
               << std::endl;
   }
