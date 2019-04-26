********************************
codecs::basic_input_range::begin
********************************

.. code-block:: cpp

   iterator begin() const;

Returns an constant iterator that can be used to retrieve the remaining input.

----

Parameters
==========

None.

Return value
============

Iterator to the remaining input's first element.

.. warning::

   The iterator is a :ref:`input_iterator`, so you should call **begin** only once or you might invalidate previously-returned iterators!

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>

   using namespace mgs;

   int main() {
      std::string s("Hello, World!");
      base64::encoder enc(s.begin(), s.end());

      auto it = enc.begin();
      assert(it == enc.begin());

      // skip one element
      auto old_it = it++;
      // old_it is invalidated
      assert(old_it != enc.begin());
      assert(it == enc.begin());
   }
