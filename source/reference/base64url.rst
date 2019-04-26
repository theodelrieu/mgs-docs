**************************
base64url, base64url_nopad
**************************

Defined in header ``<mgs/base64url.hpp>``.

.. code-block:: cpp

   class base64url;
   class base64url_nopad;

**base64url** is a codec implementing the *base64url* encoding scheme, as defined in `RFC4648 <https://tools.ietf.org/html/rfc4648>`_.

**base64url_nopad** only differs in padding policy.

----

Characteristics
===============

.. table::
   :align: left

   =================  ====================================================================
   Alphabet           ``ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-_``
   Padding            | Required by **base64url**.
                      | None when encoding, optional when decoding by **base64url_nopad**,
                      | 4 byte boundary
   Padding character  ``=``
   =================  ====================================================================

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
