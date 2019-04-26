.. _codec_traits:

********************
codecs::codec_traits
********************

Defined in header ``<mgs/codecs/concepts/codec_traits.hpp>``

.. code-block:: cpp

   // exposition only
   template <typename T, typename IS>
   using encoder = decltype(T::make_encoder(std::declval<IS>());

   // exposition only
   template <typename T, typename IS>
   using decoder = decltype(T::make_decoder(std::declval<IS>());

   template <typename T,
             typename IS1 = /* see below */, typename IS2 = /* see below */>
   concept codec_traits =
     codecs::input_source<IS1> && 
     codecs::input_source<IS2> && 
     requires(IS1 is1, IS2 is2) {
       { T::make_encoder(is1) } -> meta::input_range;
       { T::make_decoder(is2) } -> meta::input_range;
       codecs::codec_output<typename T::default_encoded_output, encoder<T, IS1>>;
       codecs::codec_output<typename T::default_decoded_output, decoder<T, IS2>>;
     };

The **codec_traits** concept specifies that a type can create encoders and decoders for a specific codec, and defines default encoded and decoded types.

----

Notation
========

* **is1** - value of type ``IS1``
* **is2** - value of type ``IS2``
* **Encoder** - type returned by ``T::make_encoder(is1)``
* **Decoder** - type returned by ``T::make_decoder(is2)``
* **E** - type alias of ``typename T::traits::default_encoded_output``
* **D** - type alias of ``typename T::traits::default_decoded_output``

Member types
============

Definitions
-----------

.. table::
   :align: left

   ========================== ==========================================================
   **default_encoded_output** Type to be used by default by a :ref:`codec` when encoding
   **default_decoded_output** Type to be used by default by a :ref:`codec` when decoding
   ========================== ==========================================================

Constraints
-----------

.. table::
   :align: left

   ========================== ====================================================
   **default_encoded_output** :ref:`codecs::codec_output\<Encoder> <codec_output>`
   **default_decoded_output** :ref:`codecs::codec_output\<Decoder> <codec_output>`
   ========================== ====================================================

Template arguments
==================

Definitions
-----------

.. table::
   :align: left

   ======= =====================================================================================================================================================
   **IS1** Type passed to ``make_encoder``, defaults to :ref:`codecs::iterator_sentinel_source\<meta::iterator_t\<D>, meta::sentinel_t\<D>> <iterator_sentinel_source>`.
   **IS2** Type passed to ``make_decoder``, defaults to :ref:`codecs::iterator_sentinel_source\<meta::iterator_t\<E>, meta::sentinel_t\<E>> <iterator_sentinel_source>`.
   ======= =====================================================================================================================================================

Constraints
-----------

.. table::
   :align: left

   ======= ===================
   **IS1** :ref:`input_source`
   **IS2** :ref:`input_source`
   ======= ===================

Valid expressions
=================

.. table::
   :align: left

   ======================== ==================
   Expression               Return type
   ======================== ==================
   **T::make_encoder(is1)** :ref:`input_range`
   **T::make_decoder(is2)** :ref:`input_range`
   ======================== ==================


Expression semantics
====================

.. table::
   :align: left

   ======================== ========================================
   Expression               Semantics
   ======================== ========================================
   **T::make_encoder(is1)** Creates an encoder from the input source
   **T::make_decoder(is2)** Creates a decoder from the input source
   ======================== ========================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T,
             typename IS1 = /* ... */, typename IS2 = /* ... */>
   struct is_codec_traits { /* ... */ };

   template <typename T,
             typename IS1 = /* ... */, typename IS2 = /* ... */>
   constexpr auto is_codec_traits_v = is_codec_traits<T, IS1, IS2>::value;

   template <typename T,
             typename IS1 = /* ... */, typename IS2 = /* ... */,
             typename = std::enable_if_t<is_codec_traits_v<T, IS1, IS2>>>
   using codec_traits = T;

   } // namespace codecs
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <string>
   #include <vector>

   #include <mgs/codecs/concepts/codec_traits.hpp>
   #include <mgs/codecs/basic_input_range.hpp>

   using namespace mgs;
   using namespace mgs::codecs;

   class noop_traits {
   private:
     using input_source = iterator_sentinel_source<char const*>;
     using noop_encoder = basic_input_range<input_source>;
     using noop_decoder = noop_encoder

   public:
     using default_encoded_output = std::string;
     using default_decoded_output = default_encoded_output;


     static noop_encoder make_encoder(input_source is) {
        return noop_encoder(is); 
     }

     static noop_decoder make_decoder(input_source is) {
        return noop_decoder(is); 
     }
   };

   int main() {
     static_assert(is_codec_traits_v<noop_traits>::value, "");
   }

See also
========

* :ref:`iterator_t`
* :ref:`sentinel_t`
* :ref:`iterator_sentinel_source`
* :ref:`input_range`
* :ref:`codec_output`
* :ref:`input_source`
* :ref:`same_as`
