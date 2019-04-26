***********************************
codecs::basic_input_range::iterator
***********************************

.. code-block:: cpp

   using iterator = /* implementation-defined */;

The iterator type, models :ref:`input_iterator`.

----

Two iterators will compare equal if and only if both are valid or both are invalid,
regardless of the range they are attached to.

.. note::

   This is the same behavior than :cpp:`std::istreambuf_iterator::equal <iterator/istreambuf_iterator/equal>`
