.. _prority_tag:

******************
meta::priority_tag
******************

Defined in header ``<mgs/meta/priority_tag.hpp>``.

.. code-block:: cpp

   template <std::size_t N>
   struct priority_tag : priority_tag<N - 1> {};

   template <>
   struct priority_tag<0> {};

**priority_tag** is a helper type used to assign a priority to overloads in an overload set.

.. tip::

   Take a look :ref:`here <using-type-aliases>` for an example.
