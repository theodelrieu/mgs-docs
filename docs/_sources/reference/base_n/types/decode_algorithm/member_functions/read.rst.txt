******************************
base_n::decode_algorithm::read
******************************

.. code-block:: cpp

   template <meta::output_iterator<element_type> O>
   std::pair<O, mgs::ssize_t> read(O dst, mgs::ssize_t n);

Fills *dst* with at most *n* bytes of decoded output, returning a pair containing the new value of *dst* and the number of bytes written.

----

Template parameters
===================

.. table::
   :align: left

   ====== ===========================================================================
   Name   Description
   ====== ===========================================================================
   **O**  | Output iterator where decoded bytes will be written.
          | Must model :ref:`meta::output_iterator\<element_type> <output_iterator>`.
   ====== ===========================================================================

Parameters
==========

* **dst** - output iterator
* **n** - maximum number of bytes to write

Return value
============

A pair containing the new position of *dst*, and the number of bytes written.

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
     std::string buffer(1024, 0);

     auto it = &buffer[0];
     auto size_to_read = buffer.size();
     auto total_read = 0;
     for (auto res = algo.read(it, size_to_read); res.second != 0;
          res = algo.read(it, size_to_read)) {
       it = res.first;
       size_to_read -= res.second;
       total_read += res.second;
     }
     buffer.resize(total_read);
     std::cout << buffer << std::endl;
   }
