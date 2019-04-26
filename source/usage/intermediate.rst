Intermediate usage
==================

This section introduces encoders and decoders.

Encoders and decoders
---------------------

Every codec is built on top of an encoder and a decoder.

They both model the :ref:`input_source` concept and thus allow lazy encoding/decoding.

To create them, use the codec traits' ``make_encoder``/``make_decoder`` static member functions.
Then, use the ``read`` member function to read sequences of elements.

.. code-block:: cpp

   #include <string>

   #include <mgs/base64.hpp>

   using namespace mgs;

   int main() {
     std::string const decoded_string("decoded");
     // retrieves the exact encoded size
     auto const encoded_size = base64::encoded_size(decoded_string.size());

     std::string encoded_string(encoded_size, 0);
     auto encoder = base64::make_encoder(decoded_string);

     auto size_to_read = encoded_size;
     auto read_result = encoder.read(encoded_string.begin(), size_to_read);

     while (read_result.second != 0) {
       size_to_read -= read_result.second;
       read_result = encoder.read(read_result.first, size_to_read);
     }
   }

In the above example, ``read`` will attempt to read ``size_to_read`` elements into an iterator.

However, implementation is allowed to read less than ``size_to_read``, which means subsequent calls to ``read`` might be necessary to read all data.

For that matter, ``read`` returns a pair containing:

* the iterator pointing after the last written element
* the number of elements written, ``0`` being EOF

.. warning::

   Encoders and decoders are stateful objects designed for one-time use, be careful to not reuse them!

Encoders as input ranges
^^^^^^^^^^^^^^^^^^^^^^^^

*mgs* provides a way to wrap a :ref:`input_source` into a :ref:`input_range`.

Though less efficient, this reduces the amount of code needed to read from a :ref:`input_source`:

.. code-block:: cpp

   #include <algorithm>
   #include <iostream>
   #include <utility>

   #include <mgs/base64.hpp>
   #include <mgs/codecs/basic_input_range.hpp>

   using namespace mgs;

   int main() {
     auto encoder = base64::make_encoder("decoded");
     auto encoding_range = codecs::make_input_range(std::move(encoder));

     // STL algorithms can be used with input ranges' iterators
     std::copy(encoding_range.begin(), encoding_range.end(),
               std::ostreambuf_iterator<char>(std::cout));
   }

.. tip::

   While more verbose, using ``read`` is usually faster than using iterators.

When to use encoders?
---------------------

.. _adding-support-for-user-defined-types:

Adding support for user-defined types
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Although *mgs* supports quite a few return types, you might use one in your code that is not supported by default.

Customizing the libary for that type requires using encoders/decoders along with the :ref:`output_traits` customization point.

As an example, here is the code needed for `QLinkedList`_:

.. code-block:: cpp

   #include <mgs/codecs/output_traits_fwd.hpp>
   #include <mgs/codecs/basic_input_range.hpp>
   #include <mgs/base64.hpp>

   #include <QLinkedList>

   #include <algorithm>
   #include <iterator>

   namespace mgs {
   namespace codecs {

   template <typename CharT>
   struct output_traits<QLinkedList<CharT>> {

     // In this case, InputSource is either an encoder or a decoder
     template <typename InputSource>
     static QLinkedList<CharT> create(InputSource source) {
       QLinkedList<CharT> list;
       // not the most efficient way
       auto range = make_input_range(std::move(source));
       std::copy(range.begin(), range.end(), std::back_inserter(list));
       return list;
     }
   };

   } // namespace codecs
   } // namespace mgs

   int main() {
     auto encoded_qlist = mgs::base64::encode<QLinkedList<char>>("Hello, World!");
   }

.. note::

   :ref:`output_traits` has a second template parameter, defaulted to ``void``, which can be used to perform SFINAE checks. 

Limiting memory usage
^^^^^^^^^^^^^^^^^^^^^

When dealing with huge volumes of data, memory consumption can become a problem.

Using the API shown in the :ref:`basic section <usage-basic>` demonstrates it well:

.. code-block:: cpp

   #include <fstream>

   #include <mgs/base64.hpp>

   using namespace mgs;

   int main() {
     // Could be a few TB...
     std::ifstream enormous_file("TODO.txt");
     std::istreambuf_iterator<char> begin(enormous_file);
     std::istreambuf_iterator<char> end;

     // oops, likely to throw
     std::vector<char> content(begin, end);
     // oops, even more likely to throw
     auto encoded = base64::encode(content);

     // very unlikely to be reached
     std::ofstream ofs("TODO.b64");
     ofs.write(encoded.c_str(), encoded.size());
   }

In this case, :cpp:`std::bad_alloc <memory/new/bad_alloc>` will likely be thrown when constructing ``content`` or ``encoded``. 

Here is how to handle it properly:

.. code-block:: cpp

   #include <algorithm>
   #include <fstream>

   #include <mgs/base64.hpp>
   #include <mgs/codecs/basic_input_range.hpp>

   using namespace mgs;

   int main() {
     std::ifstream enormous_file("TODO.txt");
     std::istreambuf_iterator<char> begin(enormous_file);
     std::istreambuf_iterator<char> end;

     auto encoder = base64::make_encoder(begin, end);
     auto encoding_range = codecs::make_input_range(std::move(encoder));

     std::ofstream ofs("TODO.b64");
     std::copy(encoding_range.begin(), encoding_range.end(),
               std::ostreambuf_iterator<char>(ofs));
   }

.. _QLinkedList: http://doc.qt.io/qt-5/qlinkedlist.html
