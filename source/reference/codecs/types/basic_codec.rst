.. _basic_codec:

*******************
codecs::basic_codec
*******************

Defined in header ``<mgs/codecs/basic_codec.hpp>``.

.. code-block:: cpp

   template <codecs::codec_traits Traits>
   class basic_codec;

The class template **basic_codec** provides a generic implementation that models the :ref:`codec` concept.

The definitions of the encoding/decoding operations are supplied via the template parameter, which must model :ref:`codec_traits`.

----

Template parameters
===================

.. table::
   :align: left

   ========== ============================================
   Name       Description
   ========== ============================================
   **Traits** Codec traits, must model :ref:`codec_traits`
   ========== ============================================

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

   encode <basic_codec/member_functions/encode>
   decode <basic_codec/member_functions/decode>
   lazy_encode <basic_codec/member_functions/lazy_encode>
   lazy_decode <basic_codec/member_functions/lazy_decode>
   make_encoder <basic_codec/member_functions/make_encoder>
   make_decoder <basic_codec/member_functions/make_decoder>

.. table::
   :align: left

   ======================================================================== ====================
   Name                                                                     Description
   ======================================================================== ====================
   :doc:`encode <basic_codec/member_functions/encode>` [static]             Encodes input
   :doc:`decode <basic_codec/member_functions/decode>` [static]             Decodes input
   :doc:`lazy_encode <basic_codec/member_functions/lazy_encode>` [static]   Lazily encodes input
   :doc:`lazy_decode <basic_codec/member_functions/lazy_decode>` [static]   Lazily decodes input
   :doc:`make_encoder <basic_codec/member_functions/make_encoder>` [static] Creates an encoder
   :doc:`make_decoder <basic_codec/member_functions/make_decoder>` [static] Creates a decoder
   ======================================================================== ====================
