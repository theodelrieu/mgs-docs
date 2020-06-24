.. _iter_rvalue_reference_t:

*****************************
meta::iter_rvalue_reference_t
*****************************

Defined in header ``<mgs/meta/iter_rvalue_reference_t.hpp>``.

.. code-block:: cpp

   template <meta::dereferenceable T>
   using iter_rvalue_reference_t = /* see below */;

Pre-C++20 implementation of :cpp:`std::iter_rvalue_reference_t <iterator/iter_t>`.

----

Differences with the C++20 version
==================================

* There is no `iter_move <https://timsong-cpp.github.io/cppwp/ranges-ts/iterator.custpoints.iter_move#1.1>`_ customization point.
* The implementation relies on `bullet 1.2 <https://timsong-cpp.github.io/cppwp/ranges-ts/iterator.custpoints.iter_move#1.2>`_.

See also
========

* :ref:`dereferenceable`
