.. _range_value_t:

*******************
meta::range_value_t
*******************

Defined in header ``<mgs/meta/range_value_t.hpp>``.

.. code-block:: cpp

   template <meta::range R>
   using range_value_t = meta::iter_value_t<meta::iterator_t<R>>;

Compute the associated *value type* of a range's iterator type.

----

See also
========

* :ref:`iter_value_t`
* :ref:`iterator_t`
* :ref:`range`
