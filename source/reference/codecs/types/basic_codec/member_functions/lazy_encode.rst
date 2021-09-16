********************************
codecs::basic_codec::lazy_encode
********************************

.. code-block:: cpp

   template <typename T = traits::default_encoded_output>
   static /* unspecified */ lazy_encode();

Returns a function object that encodes input.

-------

The returned function object has the same constraints as :ref:`codecs-encode`.

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
     std::string decoded("Hello, World!");
     auto input_source = make_iterator_sentinel_source(decoded);

     codec::lazy_encode()(input_source);
     codec::lazy_encode()(decoded.begin(), decoded.end());
     codec::lazy_encode()(decoded);
     codec::lazy_encode()(std::move(decoded));
   }

