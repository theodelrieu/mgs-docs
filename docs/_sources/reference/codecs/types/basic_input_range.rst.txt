.. _basic_input_range:

*************************
codecs::basic_input_range
*************************

Defined in header ``<mgs/codecs/basic_input_range.hpp>``.

.. code-block:: cpp

   template <codecs::input_source IS>
   class basic_input_range;

The class template **basic_input_range** wraps a :ref:`input_source` and models :ref:`input_range`.

----

Template parameters
===================

.. table::
   :align: left

   ====== ============================================================
   **IS** The underlying input source, must model :ref:`input_source`.
   ====== ============================================================

Models
======

* :ref:`input_range`

Member types
============

.. toctree::
   :hidden:
   :titlesonly:

   iterator <basic_input_range/types/iterator>

.. table::
   :align: left

   ========================================================== =================
   Name                                                       Description
   ========================================================== =================
   :doc:`iterator <basic_input_range/types/iterator>`         The iterator type
   ========================================================== =================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:

   (constructor) <basic_input_range/member_functions/constructor>
   begin <basic_input_range/member_functions/begin>
   end <basic_input_range/member_functions/end>

.. table::
   :align: left

   ================================================================================= ===============================
   Name                                                                              Description
   ================================================================================= ===============================
   :doc:`\(constructor\) <basic_input_range/member_functions/constructor>`           Constructor
   :doc:`begin <basic_input_range/member_functions/begin>`                           Get begin iterator
   :doc:`end <basic_input_range/member_functions/end>`                               Get end iterator
   ================================================================================= ===============================
