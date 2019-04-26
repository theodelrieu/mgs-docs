.. _encode_algorithm:

************************
base_n::encode_algorithm
************************

Defined in header ``<mgs/base_n/encode_algorithm.hpp>``.

.. code-block:: cpp

   template <base_n::encoding_traits Traits, codecs::input_source IS>
      requires Traits::padding_policy != padding_policy::optional
   class encode_algorithm;

The class template **encode_algorithm** provides a generic implementation for BaseN encoding, and models :ref:`input_source`.

The encoding's characteristics are provided via the **Traits** template parameter.

.. note::

   `encode_algorithm` will model :ref:`sized_input_source` if **IS** models it.

----

Valid padding policies are:

* **padding_policy::none** - Output will not be padded.
* **padding_policy::required** - Output will be padded.

.. note::

   **padding_policy::optional** does not make sense when encoding.


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

   (constructor) <encode_algorithm/member_functions/constructor>
   read <encode_algorithm/member_functions/read>
   max_remaining_size <encode_algorithm/member_functions/max_remaining_size>

.. table::
   :align: left

   ================================================================================ ==============================================
   Name                                                                             Description
   ================================================================================ ==============================================
   :doc:`\(constructor\) <encode_algorithm/member_functions/constructor>`           Constructs an algorithm function object
   :doc:`read <encode_algorithm/member_functions/read>`                             Fills a buffer with encoded output
   :doc:`max_remaining_size <encode_algorithm/member_functions/max_remaining_size>` Computes the maximum number of remaining bytes
   ================================================================================ ==============================================
