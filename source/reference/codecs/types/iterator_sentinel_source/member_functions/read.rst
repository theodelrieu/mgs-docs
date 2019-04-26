**************************************
codecs::iterator_sentinel_source::read
**************************************

.. code-block:: cpp

   template <meta::output_iterator<element_type> O>
   std::pair<O, mgs::ssize_t> read(O dst, mgs::ssize_t n);

Fills *dst* with at most *n* bytes of input, returning a pair containing the new value of *dst* and the number of bytes written.

----

Parameters
==========

* **dst** - output iterator
* **n** - maximum number of bytes to write

Return value
============

A pair containing the new position of *dst*, and the number of bytes written.

Example
=======

.. code-block:: cpp

   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;
   using namespace mgs::codecs;

   int main() {
     std::string hello("Hello, World!");
     auto input_source = make_iterator_sentinel_source(hello);

     std::vector<unsigned char> buffer(hello.size());
     auto it = buffer.data();
     auto size_to_read = buffer.size();
     auto total_read = 0;
     for (auto res = input_source.read(it, size_to_read);
          res.second != 0;
          res = input_source.read(it, size_to_read))
     {
       it = res.first;
       size_to_read -= res.second;
       total_read += res.second;
     }
   }
