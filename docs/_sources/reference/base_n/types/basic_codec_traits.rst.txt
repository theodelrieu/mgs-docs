**************************
base_n::basic_codec_traits
**************************

Defined in header ``<mgs/base_n/basic_codec_traits.hpp>``.

.. code-block:: cpp

   template <base_n::encoding_traits EncoderTraits,
             base_n::encoding_traits DecoderTraits = EncoderTraits>
   class basic_codec_traits;

The class template **basic_codec_traits** provides a generic traits class for every BaseN codec, modeling the :ref:`codec_traits` concept.

----

Template parameters
===================

.. table::
   :align: left

   ================= ========================================================================
   Name              Description
   ================= ========================================================================
   **EncoderTraits** Encoding traits used to encode input, must model :ref:`encoding_traits`.
   **DecoderTraits** Encoding traits used to decode input, defaulted to **EncoderTraits**.
   ================= ========================================================================

Member types
============

.. toctree::
   :hidden:
   :titlesonly:

   default_encoded_output <basic_codec_traits/types/default_encoded_output>
   default_decoded_output <basic_codec_traits/types/default_decoded_output>

.. table::
   :align: left

   =============================================================================== =================================
   Name                                                                            Description
   =============================================================================== =================================
   :doc:`default_encoded_output <basic_codec_traits/types/default_encoded_output>` Default type returned by encoders
   :doc:`default_decoded_output <basic_codec_traits/types/default_decoded_output>` Default type returned by decoders
   =============================================================================== =================================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:

   make_encoder <basic_codec_traits/member_functions/make_encoder>
   make_decoder <basic_codec_traits/member_functions/make_decoder>

.. table::
   :align: left

   =============================================================================== =====================
   Name                                                                            Description
   =============================================================================== =====================
   :doc:`make_encoder <basic_codec_traits/member_functions/make_encoder>` [static] Constructs an encoder
   :doc:`make_decoder <basic_codec_traits/member_functions/make_decoder>` [static] Constructs a decoder
   =============================================================================== =====================
