.. _range_difference_t:

************************
meta::range_difference_t
************************

Defined in header ``<mgs/meta/range_difference_t.hpp>``.

.. code-block:: cpp

   template <Range R>
   using range_difference_t = iter_difference_t<iterator_t<R>>;

Compute the associated *difference type* of a range's iterator type.

----

See also
========

* :ref:`iter_difference_t`
* :ref:`iterator_t`
* :ref:`range`
