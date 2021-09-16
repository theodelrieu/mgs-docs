********************************
codecs::basic_codec::lazy_decode
********************************

.. code-block:: cpp

   template <typename T = traits::default_decoded_output>
   static /* unspecified */ lazy_decode();

Returns a function object that decodes input.

-------

The returned function object has the same constraints as :ref:`codecs-decode`.

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>
   #include <mgs/codecs/basic_codec.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;
   using namespace mgs::codecs;

   using codec = basic_codec<base64::traits>;

   int main() {
     std::string encoded("SGVsbG8sIFdvcmxkIQ==");
     auto input_source = make_iterator_sentinel_source(encoded);

     codec::lazy_decode()(input_source);
     codec::lazy_decode()(encoded.begin(), encoded.end());
     codec::lazy_decode()(encoded);
     codec::lazy_decode()(std::move(encoded));
   }

