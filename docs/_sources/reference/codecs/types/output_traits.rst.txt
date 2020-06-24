.. _output_traits:

*********************
codecs::output_traits
*********************

Declared in header ``<mgs/codecs/output_traits_fwd.hpp>``.

Defined in header ``<mgs/codecs/output_traits.hpp>``.

.. code-block:: cpp

   template <typename T, typename SFINAE = void>
   class output_traits;

The class template **output_traits** is a customization point that users can extend in order to make their types model :ref:`codec_output`.

.. note::

   This section will only document the default implementation (i.e. primary specialization).

   Look :ref:`here <adding-support-for-user-defined-types>` to learn how to specialize it for your own types.

----

Template arguments
==================

.. table::
   :align: left

   ========== =============================================================================
   Name       Description
   ========== =============================================================================
   **T**      Type to be returned by :doc:`create <output_traits/member_functions/create>`.
   **SFINAE** Placeholder, useful when adding constraints in a specialization.
   ========== =============================================================================

Member functions
================

.. toctree::
   :hidden:
   :titlesonly:
   
   create <output_traits/member_functions/create>

.. table::
   :align: left

   ============================================================== =========================================================
   Name                                                           Description
   ============================================================== =========================================================
   :doc:`create <output_traits/member_functions/create>` [static] Returns a type containing a :ref:`input_range` 's content
   ============================================================== =========================================================

Member types
============

.. toctree::
   :hidden:
   :titlesonly:
   
   output_type <output_traits/types/output_type>

.. table::
   :align: left

   ==================================================== =======================================================================
   Name                                                 Description
   ==================================================== =======================================================================
   :doc:`output_type <output_traits/types/output_type>` Type returned by :doc:`create <output_traits/member_functions/create>`.
   ==================================================== =======================================================================
