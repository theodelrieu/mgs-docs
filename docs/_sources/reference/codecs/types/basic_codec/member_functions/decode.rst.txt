.. _codecs-decode:

***************************
codecs::basic_codec::decode
***************************

.. code-block:: cpp

   // exposition only
   template <typename ...Ts>
   using Decoder = decltype(make_decoder(std::declval<Ts>()...));

   template <typename T = traits::default_decoded_output,
             codecs::input_source IS>
      requires codecs::codec_output<T, Decoder<IS>>
   static T decode(IS is);                                  // (1)

   template <typename T = traits::default_decoded_output,
             meta::input_iterator I,
             meta::sentinel_for<I> S>
      requires codecs::codec_output<T, Decoder<I, S>>
   static T decode(I i, S s);                               // (2)

   template <typename T = traits::default_decoded_output,
             meta::input_range R>
      requires codecs::codec_output<T, Decoder<R>>
   static T decode(R& rng);                                 // (3)

   template <typename T = traits::default_decoded_output,
             meta::input_range R>
      requires codecs::codec_output<T, Decoder<R const>>
   static T decode(R const& rng);                           // (4)

Decodes input.

-------

All these overloads will **only** participate in overload resolution if calling :ref:`codecs-make_decoder` with the same arguments is valid.

#. Decodes the content of the input source ``is``.
#. Decodes the content of the iterator-sentinel range *[i, s)* and returns the result as a **T**.
#. Decodes the content of ``rng``, and returns the result as a **T**.
#. Same as (3), but allows rvalues and const lvalues to be passed.

Parameters
==========

* **is** - Input source
* **rng** - Input range
* **i**, **s** - Iterator/sentinel input range

Return value
============

A value containing the decoded output

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

     codec::decode(input_source);                   // (1)
     codec::decode(encoded.begin(), encoded.end()); // (2)
     codec::decode(encoded);                        // (3)
     codec::decode(std::move(encoded));             // (4)
   }

