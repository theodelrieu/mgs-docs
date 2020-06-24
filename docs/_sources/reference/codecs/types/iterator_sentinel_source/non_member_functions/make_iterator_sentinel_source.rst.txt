*************************************
codecs::make_iterator_sentinel_source
*************************************

.. code-block:: cpp

   template <meta::input_iterator I, meta::sentinel_for<I> S>
   iterator_sentinel_source make_iterator_sentinel_source(I begin, S end); // (1)

   template <meta::input_range R>
   iterator_sentinel_source make_iterator_sentinel_source(R& range);       // (2)

   template <meta::input_range R>
   iterator_sentinel_source make_iterator_sentinel_source(R const& range); // (3)

----

#. Construct a ``iterator_sentinel_source`` wrapping ``begin`` and ``end``.

    This overload only participates in overload resolution if:
      * **I** models :ref:`input_iterator`
      * **S** models :ref:`meta::sentinel_for\<I> <sentinel_for>`

#. Construct a ``iterator_sentinel_source`` wrapping ``range``, and returns the result as a **T**.

    This overload only participates in overload resolution if:
      * **R** models :ref:`input_range`

#. Same as (2), but allows rvalues and const lvalues to be passed.

Parameters
==========

* **begin**, **end** - Iterator/sentinel input range
* **range** - Input range
