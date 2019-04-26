****************************************************
codecs::iterator_sentinel_source::max_remaining_size
****************************************************

.. code-block:: cpp

   mgs::ssize_t max_remaining_size() const;

Computes the maximum number of remaining bytes.

----

Constraints
===========

This function is only defined if **S** models :ref:`meta::sized_sentinel_for\<I> <sized_sentinel_for>`.

Parameters
==========

None.

Return value
============

The maximum number of remaining bytes.

Example
=======

.. code-block:: cpp

   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs::codecs;

   int main() {
     std::string hello("Hello, World!");

     auto input_source = make_iterator_sentinel_source(hello);
     auto size = input_source.max_remaining_size();
   }
