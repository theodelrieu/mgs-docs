.. _iterator_sentinel_source:

********************************
codecs::iterator_sentinel_source
********************************

Defined in header ``<mgs/codecs/iterator_sentinel_source.hpp>``.

.. code-block:: cpp

   template <meta::input_iterator I, meta::sentinel_for<I> S = I>
   class iterator_sentinel_source;

The class template **iterator_sentinel_source** models :ref:`input_source` by wrapping a :ref:`input_iterator` and a :ref:`sentinel_for`.

----

Template parameters
===================

.. table::
   :align: left

   ===== ===================
   Name  Description
   ===== ===================
   **I** Input iterator type
   **S** Sentinel type
   ===== ===================

Member types
============

.. toctree::
   :hidden:
   :titlesonly:

   element_type <iterator_sentinel_source/types/element_type>

.. table::
   :align: left

   ================================================================= =================
   Name                                                              Description
   ================================================================= =================
   :doc:`element_type <iterator_sentinel_source/types/element_type>` The element type
   ================================================================= =================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:

   (constructor) <iterator_sentinel_source/member_functions/constructor>
   read <iterator_sentinel_source/member_functions/read>
   max_remaining_size <iterator_sentinel_source/member_functions/max_remaining_size>
   begin <iterator_sentinel_source/member_functions/begin>
   end <iterator_sentinel_source/member_functions/end>

.. table::
   :align: left

   ======================================================================================== ===============================================================
   Name                                                                                     Description
   ======================================================================================== ===============================================================
   :doc:`\(constructor\) <iterator_sentinel_source/member_functions/constructor>`           Construct an input source from an iterator/sentinel range
   :doc:`read <iterator_sentinel_source/member_functions/read>`                             Fill a :ref:`output_iterator` with the input range's content
   :doc:`max_remaining_size <iterator_sentinel_source/member_functions/max_remaining_size>` Compute the maximum number of remaining bytes
   :doc:`begin <iterator_sentinel_source/member_functions/begin>`                           Returns the stored :ref:`input_iterator`
   :doc:`end <iterator_sentinel_source/member_functions/end>`                               Returns the stored :ref:`meta::sentinel_for\<I> <sentinel_for>`
   ======================================================================================== ===============================================================

Non-member functions
====================

.. toctree::
   :hidden:
   :titlesonly:

   make_iterator_sentinel_source <iterator_sentinel_source/non_member_functions/make_iterator_sentinel_source>

.. table::
   :align: left

   ================================================================================================================== ========================================================
   Name                                                                                                               Description
   ================================================================================================================== ========================================================
   :doc:`make_iterator_sentinel_source <iterator_sentinel_source/non_member_functions/make_iterator_sentinel_source>` Helper function to create a ``iterator_sentinel_source``
   ================================================================================================================== ========================================================
