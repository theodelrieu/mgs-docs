.. _range_rvalue_reference_t:

******************************
meta::range_rvalue_reference_t
******************************

Defined in header ``<mgs/meta/range_rvalue_reference_t.hpp>``.

.. code-block:: cpp

   template <meta::range R>
   using range_rvalue_reference_t = meta::iter_rvalue_reference_t<meta::iterator_t<R>>;

Compute the associated *rvalue reference type* of a range's iterator type.

----

See also
========

* :ref:`iter_rvalue_reference_t`
* :ref:`iterator_t`
* :ref:`range`
