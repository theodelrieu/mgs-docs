.. _codecs-make_decoder:

*********************************
codecs::basic_codec::make_decoder
*********************************

.. code-block:: cpp

  template <codecs::input_source IS>
  static auto make_decoder(Is is) -> /* see below */

  template <meta::input_iterator I, meta::sentinel_for<I> S>
  static auto make_decoder(I i, S s) -> /* see below */;

  template <meta::input_range R>
  static auto make_decoder(R& rng) -> /* see below */;

  template <meta::input_range R>
  static auto make_decoder(R const& rng) -> /* see below */;

Creates a decoder.

-----

#. Creates a decoder from ``is``.

    Equivalent to ``traits::make_decoder(is)``.

    This overload only participates in overload resolution if:
      * **IS** models :ref:`input_source`.

#. Creates a decoder from the iterator-sentinel range *[i, s)*.

    Equivalent to ``traits::make_decoder(codecs::make_iterator_sentinel_source(i, s))``.

    This overload only participates in overload resolution if:
      * **I** models :ref:`input_iterator`
      * **S** models :ref:`meta::sentinel_for\<I> <sentinel_for>`

#. Creates a decoder from the range ``rng``.

    Equivalent to ``traits::make_decoder(codecs::make_iterator_sentinel_source(rng))``.

    This overload only participates in overload resolution if:
      * **R** models :ref:`input_range`.

#. Same as (3), but allows rvalues and const lvalues to be passed.

Parameters
==========

* **is** - Input source
* **rng** - Input range
* **i**, **s** - Iterator/sentinel input range

Return value
============

A decoder wrapping the input source.

Example
=======

.. code-block:: cpp

   #include <string>

   #include <mgs/base_n/basic_codec_traits.hpp>
   #include <mgs/codecs/basic_codec.hpp>
   #include <mgs/codecs/basic_input_range.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;
   using namespace mgs::base_n;
   using namespace mgs::codecs;

   namespace
   {

   struct binary_encoding_traits
   {
     // using C++17 inline variables for simplicity
     inline static char const alphabet[] = {'0', '1'};
     inline static auto const padding_policy = base_n::padding_policy::none;

     static int index_of(char c)
     {
       if (c == '0')
         return 0;
       if (c == '1')
         return 1;
       return -1;
     }
   };

   } // namespace

   using binary_traits = basic_codec_traits<binary_encoding_traits>;
   using binary_codec = basic_codec<binary_traits>;

   int main()
   {
     std::string hello(
         "010010000110010101101100011011000110111100101100001000000101011101101111"
         "01110010011011000110010000100001");

     auto input_source = codecs::make_iterator_sentinel_source(hello);
     auto decoder1 = binary_codec::make_decoder(input_source);
     auto decoder2 = binary_codec::make_decoder(hello.begin(), hello.end());
     auto decoder3 = binary_codec::make_decoder(hello);
   }
