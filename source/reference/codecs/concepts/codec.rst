.. _codec:

*************
codecs::codec
*************

Defined in header ``<mgs/codecs/concepts/codec.hpp>``

.. code-block:: cpp

   template <typename T,
             typename R1 = /* see below */, typename R2 = /* see below */,
             typename IS1 = /* see below */, typename IS2 = /* see below */>
   concept codec =
     requires(IS1 is1, IS2 is2) {
       codecs::codec_traits<typename T::traits, IS1, IS2>;

       { T::template encode<R1>(is1) } -> meta::same_as<R1>;
       { T::template decode<R2>(is2) } -> meta::same_as<R2>;
     };

----

The **codec** concept specifies the requirements of input encoding/decoding.

It is *mgs*' highest-level component.

Notation
========

* **is1** - value of type ``IS1``
* **is2** - value of type ``IS2``
* **Traits** - type of ``typename T::traits``
* **E** - type of ``typename T::traits::default_encoded_output``
* **D** - type of ``typename T::traits::default_decoded_output``

Template arguments
==================

Definitions
-----------

.. table::
   :align: left

   ======= ===============================================================================================================================================
   **R1**  Return type of ``encode``, defaults to ``typename T::traits::default_encoded_output``.
   **R2**  Return type of ``decode``, defaults to ``typename T::traits::default_decoded_output``.
   **IS1** Type passed to ``encode``, defaults to :ref:`codecs::iterator_sentinel_source\<meta::iterator_t\<D>, meta::sentinel_t\<D>> <iterator_sentinel_source>`.
   **IS2** Type passed to ``decode``, defaults to :ref:`codecs::iterator_sentinel_source\<meta::iterator_t\<E>, meta::sentinel_t\<E>> <iterator_sentinel_source>`.
   ======= ===============================================================================================================================================

Constraints
-----------

.. table::
   :align: left

   ========== =====================================================
   **Traits** :ref:`codecs::codec_traits\<IS1, IS2> <codec_traits>`
   **IS1**    :ref:`input_source`
   **IS2**    :ref:`input_source`
   ========== =====================================================

Valid expressions
=================

.. table::
   :align: left

   =============================== ===========
   Expression                      Return type
   =============================== ===========
   **T::template encode<R1>(is1)** ``R1``
   **T::template decode<R2>(is2)** ``R2``
   =============================== ===========

Expression semantics
====================

.. table::
   :align: left

   =============================== ======================================================
   Expression                      Semantics
   =============================== ======================================================
   **T::template decode<R1>(is1)** Encodes the source's input into a value of type ``R1``
   **T::template decode<R2>(is2)** Decodes the source's input into a value of type ``R2``
   =============================== ======================================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T,
             typename R1 = /* ... */, typename R2 = /* ... */,
             typename IS1 = /* ... */, typename IS2 = /* ... */>
   struct is_codec { /* ... */ };

   template <typename T,
             typename R1 = /* ... */, typename R2 = /* ... */,
             typename IS1 = /* ... */, typename IS2 = /* ... */>
   constexpr auto is_codec_v = is_codec<T, R1, R2, IS1, IS2>::value;

   template <typename T,
             typename R1 = /* ... */, typename R2 = /* ... */,
             typename IS1 = /* ... */, typename IS2 = /* ... */,
             typename = std::enable_if_t<is_codec_v<T, R1, R2, IS1, IS2>>>
   using codec = T;

   } // namespace codecs
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>
   #include <mgs/codecs/concepts/codec.hpp>

   using namespace mgs::codecs;

   int main() {
     static_assert(is_codec_v<base64>, "");
     static_assert(is_codec_v<base64, std::string, std::vector<unsigned char>>, "");
   }

See also
========

* :ref:`iterator_t`
* :ref:`sentinel_t`
* :ref:`iterator_sentinel_source`
* :ref:`codec_traits`
* :ref:`same_as`
* :ref:`input_source`
