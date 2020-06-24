.. _decode_algorithm:

************************
base_n::decode_algorithm
************************

Defined in header ``<mgs/base_n/decode_algorithm.hpp>``.

.. code-block:: cpp

   template <base_n::encoding_traits Traits, codecs::input_source IS>
   class decode_algorithm;

The class template **decode_algorithm** provides a generic implementation for BaseN decoding, and models :ref:`input_source`.

The encoding's characteristics are provided via the **Traits** template parameter.

----

Valid padding policies are:

* **padding_policy::none** - Only non-padded input is considered valid.
* **padding_policy::required** - Only padded input is considered valid.
* **padding_policy::optional** - Both padded and non-padded are considered valid.

Template parameters
===================

.. table::
   :align: left

   ========== ===================================================
   Name       Description
   ========== ===================================================
   **Traits** Encoding traits, must model :ref:`encoding_traits`.
   **IS**     Input source type, must model :ref:`input_source`.
   ========== ===================================================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:

   (constructor) <decode_algorithm/member_functions/constructor>
   read <decode_algorithm/member_functions/read>
   max_remaining_size <decode_algorithm/member_functions/max_remaining_size>

.. table::
   :align: left

   ================================================================================ ==============================================
   Name                                                                             Description
   ================================================================================ ==============================================
   :doc:`\(constructor\) <decode_algorithm/member_functions/constructor>`           Constructs an algorithm function object
   :doc:`read <decode_algorithm/member_functions/read>`                             Fills a buffer with decoded output
   :doc:`max_remaining_size <decode_algorithm/member_functions/max_remaining_size>` Computes the maximum number of remaining bytes
   ================================================================================ ==============================================
