.. _codecs-encode:

***************************
codecs::basic_codec::encode
***************************

.. code-block:: cpp

   // exposition only
   template <typename ...Ts>
   using Encoder = decltype(make_encoder(std::declval<Ts>()...));

   template <typename T = traits::default_encoded_output,
             codecs::input_source IS>
      requires codecs::codec_output<T, Encoder<IS>>
   static T encode(IS is);                                  // (1)

   template <typename T = traits::default_encoded_output,
             meta::input_iterator I,
             meta::sentinel_for<I> S>
      requires codecs::codec_output<T, Encoder<I, S>>
   static T encode(I i, S s);                               // (2)

   template <typename T = traits::default_encoded_output,
             meta::input_range R>
      requires codecs::codec_output<T, Encoder<R>>
   static T encode(R& rng);                                 // (3)

   template <typename T = traits::default_encoded_output,
             meta::input_range R>
      requires codecs::codec_output<T, Encoder<R const>>
   static T encode(R const& rng);                           // (4)

Encodes input.

-------

All these overloads will **only** participate in overload resolution if calling :ref:`codecs-make_encoder` with the same arguments is valid.

#. Encodes the content of the input source ``is``.
#. Encodes the content of the iterator-sentinel range *[i, s)* and returns the result as a **T**.
#. Encodes the content of ``rng``, and returns the result as a **T**.
#. Same as (3), but allows rvalues and const lvalues to be passed.

Parameters
==========

* **is** - Input source
* **rng** - Input range
* **i**, **s** - Iterator/sentinel input range

Return value
============

A value containing the encoded output

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

     codec::encode(input_source);                   // (1)
     codec::encode(decoded.begin(), decoded.end()); // (2)
     codec::encode(decoded);                        // (3)
     codec::encode(std::move(decoded));             // (4)
   }
