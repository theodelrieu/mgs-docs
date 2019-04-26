****************************************
base_n::basic_codec_traits::make_decoder
****************************************

.. code-block:: cpp

  template <codecs::input_source IS>
    requires codecs::byte_type<typename IS::element_type>
  static auto make_decoder(IS is) ->
      base_n::decode_algorithm<EncodingTraits, IS>;

Creates a decoder from the :ref:`input_source` ``is``.

Template parameters
===================

.. table::
   :align: left

   ====== ===================================================
   Name   Description
   ====== ===================================================
   **IS** | Input source type, must model :ref:`input_source` 
          | and ``typename IS::element_type`` must model 
          | :ref:`byte_type`.
   ====== ===================================================

Parameters
==========

* **is** - The input source

Return value
============

A decoder wrapping the input source.

Example
=======

.. code-block:: cpp

   #include <iostream>
   #include <string>

   #include <mgs/base64.hpp>
   #include <mgs/base_n/basic_codec_traits.hpp>
   #include <mgs/codecs/basic_input_range.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;
   using namespace mgs::base_n;

   namespace {

   struct binary_encoding_traits {
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

   using binary_traits = basic_codec_traits<binary_encoding_traits>;

   int main() {
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
     auto decoder = binary_traits::make_decoder(input_source);
     auto decoding_range = codecs::make_input_range(decoder);
     std::string decoded(decoding_range.begin(), decoding_range.end());
     std::cout << decoded << std::endl;
   }
