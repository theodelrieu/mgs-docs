.. _codecs-make_encoder:

*********************************
codecs::basic_codec::make_encoder
*********************************

.. code-block:: cpp

  template <codecs::input_source IS>
  static auto make_encoder(Is is) -> /* see below */

  template <meta::input_iterator I, meta::sentinel_for<I> S>
  static auto make_encoder(I i, S s) -> /* see below */;

  template <meta::input_range R>
  static auto make_encoder(R& rng) -> /* see below */;

  template <meta::input_range R>
  static auto make_encoder(R const& rng) -> /* see below */;

Creates an encoder.

-----

#. Creates an encoder from ``is``.

    Equivalent to ``traits::make_encoder(is)``.

    This overload only participates in overload resolution if:
      * **IS** models :ref:`input_source`.

#. Creates an encoder from the iterator-sentinel range *[i, s)*.

    Equivalent to ``traits::make_encoder(codecs::make_iterator_sentinel_source(i, s))``.

    This overload only participates in overload resolution if:
      * **I** models :ref:`input_iterator`
      * **S** models :ref:`meta::sentinel_for\<I> <sentinel_for>`

#. Creates an encoder from the range ``rng``.

    Equivalent to ``traits::make_encoder(codecs::make_iterator_sentinel_source(rng))``.

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

An encoder wrapping the input source.

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
     std::string hello("Hello, World!");

     auto input_source = codecs::make_iterator_sentinel_source(hello);
     auto encoder1 = binary_codec::make_encoder(input_source);                // (1)
     auto encoder2 = binary_codec::make_encoder(hello.begin(), hello.end());  // (2)
     auto encoder3 = binary_codec::make_encoder(hello);                       // (3)
   }
