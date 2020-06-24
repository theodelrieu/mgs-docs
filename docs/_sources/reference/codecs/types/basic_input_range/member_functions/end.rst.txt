******************************
codecs::basic_input_range::end
******************************

.. code-block:: cpp

   iterator end() const;

Returns an iterator acting as a sentinel

----

Parameters
==========

None

Return value
============

A sentinel

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>

   using namespace mgs;

   int main() {
     std::string s("Hello, world!");
     auto enc = base64::make_encoder(s.begin(), s.end());

     for (auto c : enc) { /* ... */ }

     assert(enc.begin() == enc.end());
   }
