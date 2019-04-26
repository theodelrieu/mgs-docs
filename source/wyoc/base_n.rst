===================
Write a BaseN codec
===================

This section explains how to create BaseN codec variants (e.g. :doc:`/reference/base64` with a different alphabet).

Define your encoding traits
---------------------------

To create your codec variant, you first need to define an encoding traits type, which must model :ref:`encoding_traits`.

Here are the :doc:`/reference/base64` traits (simplified):

.. code-block:: cpp

   #include <algorithm>

   #include <mgs/base_n/padding_policy.hpp>

   using namespace mgs;

   struct base64_encoding_traits
   {
     using alphabet_t = char const[64];

     // using C++17 inline variables for simplicity
     inline static constexpr alphabet_t alphabet = {
         'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
         'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z',
         'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm',
         'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
         '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '+', '/'};

     inline static constexpr char padding_character = '=';
     inline static constexpr auto padding_policy =
         base_n::padding_policy::required;

     // must return the position of the parameter in the alphabet, or -1
     static constexpr int index_of(char c)
     {
       auto it = std::find(std::begin(alphabet), std::end(alphabet), c);
       if (it == std::end(alphabet))
         return -1;
       return it - std::begin(alphabet);
     }
   };

.. tip::

   For better performance, I recommend using a lookup-table instead of relying on :cpp:`std::find <algorithm/find>`.

Create the codec variant
------------------------

*mgs* uses a generic implementation for every BaseN codec, which can be parameterized with encoding traits:

.. code-block:: cpp

   // Header <mgs/base_n/basic_codec.hpp>

   namespace mgs {
   namespace base_n {

   template <typename EncodingTraits,
             typename DecodingTraits = EncodingTraits>
   class basic_codec { /* ... */ };

   } // namespace base_n
   } // namespace mgs

You have to instantiate it with your encoding traits:

.. code-block:: cpp

   #include <algorithm>
   #include <iostream>

   #include <mgs/base_n/basic_codec.hpp>
   #include <mgs/base_n/padding_policy.hpp>

   using namespace mgs;

   struct base64_encoding_traits {
     using alphabet_t = char const[64];

     // using C++17 inline variables for simplicity
     inline static constexpr alphabet_t alphabet = {
         'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
         'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z',
         'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm',
         'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
         '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '+', '/'};

     inline static constexpr char padding_character = '=';
     inline static constexpr auto padding_policy =
         base_n::padding_policy::required;

     // must return the position of the parameter in the alphabet, or -1
     static int index_of(char c) {
       auto it = std::find(std::begin(alphabet), std::end(alphabet), c);
       if (it == std::end(alphabet)) return -1;
       return it - std::begin(alphabet);
     }
   };

   int main() {
     using custom_base64 = base_n::basic_codec<base64_encoding_traits>;

     std::cout << custom_base64::encode("Hello, World!") << std::endl;
   }

.. note::

   :ref:`base_n-basic_codec` second template parameter is useful if you want to have different behaviors when encoding and decoding (e.g. :doc:`base64url_nopad </reference/base64url>` has different padding policies).
