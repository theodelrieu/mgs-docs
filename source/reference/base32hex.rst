*********
base32hex
*********

Defined in header ``<mgs/base32hex.hpp>``.

.. code-block:: cpp

   class base32hex;

**base32hex** is a codec implementing the *base32hex* encoding scheme, as defined in `RFC4648 <https://tools.ietf.org/html/rfc4648>`_.

----

Characteristics
===============

.. table::
   :align: left

   =================  ====================================
   Alphabet           ``0123456789ABCDEFGHIJKLMNOPQRSTUV``
   Padding            Required, 8 byte boundary
   Padding character  ``=``
   =================  ====================================

Inherited from :doc:`base_n::basic_codec <base_n/types/basic_codec>`
====================================================================

Member types
------------

.. toctree::
   :hidden:
   :titlesonly:

   traits <base_n/types/basic_codec/types/traits>

.. table::
   :align: left

   ======================================================= ================
   Name                                                    Description
   ======================================================= ================
   :doc:`traits <base_n/types/basic_codec/types/traits>`   The codec traits
   ======================================================= ================

Member functions
----------------

.. toctree::
   :hidden:
   :titlesonly:

   encoded_size <base_n/types/basic_codec/member_functions/encoded_size>
   max_decoded_size <base_n/types/basic_codec/member_functions/max_decoded_size>

.. table::

   ============================================================================================= =======================================================
   Name                                                                                          Description
   ============================================================================================= =======================================================
   :doc:`encoded_size <base_n/types/basic_codec/member_functions/encoded_size>` [static]         Computes the encoded size given a decoded size
   :doc:`max_decoded_size <base_n/types/basic_codec/member_functions/max_decoded_size>` [static] Computes the maximum decoded size given an encoded size
   ============================================================================================= =======================================================

Inherited from :doc:`codecs::basic_codec <codecs/types/basic_codec>`
====================================================================

Member functions
----------------

.. table::
   :align: left

   ========================================================================= =============
   Name                                                                      Description
   ========================================================================= =============
   :doc:`encode <codecs/types/basic_codec/member_functions/encode>` [static] Encodes input
   :doc:`decode <codecs/types/basic_codec/member_functions/decode>` [static] Decodes input
   ========================================================================= =============
