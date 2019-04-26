.. _base_n-basic_codec:

*******************
base_n::basic_codec
*******************

Defined in header ``<mgs/base_n/basic_codec.hpp>``.

.. code-block:: cpp

   template <base_n::encoding_traits EncoderTraits,
             base_n::encoding_traits DecoderTraits = EncoderTraits>
   class basic_codec;

The class template **basic_codec** provides a generic implementation of BaseN codecs, that models the :ref:`codec` concept.

The definitions of the encoding/decoding operations are supplied via the template parameters, which must model :ref:`encoding_traits`.

----

Template parameters
===================

.. table::
   :align: left

   ================= =======================================================================
   Name              Description
   ================= =======================================================================
   **EncoderTraits** Encoding traits used to encode input, must model :ref:`encoding_traits`
   **DecoderTraits** Encoding traits used to decode input, defaulted to **EncoderTraits**
   ================= =======================================================================

Member types
============

.. toctree::
   :hidden:
   :titlesonly:

   traits <basic_codec/types/traits>

.. table::
   :align: left

   ========================================== ================
   Name                                       Description
   ========================================== ================
   :doc:`traits <basic_codec/types/traits>`   The codec traits
   ========================================== ================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:

   encoded_size <basic_codec/member_functions/encoded_size>
   max_decoded_size <basic_codec/member_functions/max_decoded_size>

.. table::

   ================================================================================ =======================================================
   Name                                                                             Description
   ================================================================================ =======================================================
   :doc:`encoded_size <basic_codec/member_functions/encoded_size>` [static]         Computes the encoded size given a decoded size
   :doc:`max_decoded_size <basic_codec/member_functions/max_decoded_size>` [static] Computes the maximum decoded size given an encoded size
   ================================================================================ =======================================================

Inherited from :ref:`basic_codec`
=================================

Member functions
----------------

.. table::
   :align: left

   ================================================================================================ ==================
   Name                                                                                             Description
   ================================================================================================ ==================
   :doc:`encode </reference/codecs/types/basic_codec/member_functions/encode>` [static]             Encodes input
   :doc:`decode </reference/codecs/types/basic_codec/member_functions/decode>` [static]             Decodes input
   :doc:`make_encoder </reference/codecs/types/basic_codec/member_functions/make_encoder>` [static] Creates an encoder
   :doc:`make_decoder </reference/codecs/types/basic_codec/member_functions/make_decoder>` [static] Creates a decoder
   ================================================================================================ ==================
