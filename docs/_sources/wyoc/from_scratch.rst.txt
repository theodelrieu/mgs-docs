==========================
Write a codec from scratch
==========================

This section introduces building blocks that can be used to create codecs from scratch.

Write an input source
---------------------

Input sources are *mgs*' lowest level constructs. Their role is to provide sequential reads of arbitrary input.

They must model :ref:`input_source`.

Let's write a simple one, that will only work with ``char const*``:

.. code-block:: cpp

   #include <algorithm>
   #include <utility>

   #include <mgs/ssize_t.hpp>

   class noop_encoder {
    public:
     using element_type = char;

     noop_encoder(char const* begin, char const* end) : _current(begin), _end(end) {}

     template <typename O>
     std::pair<O, int> read(O dst, int max_length) {
       auto const to_read =
           std::min<int>(max_length, std::distance(_current, _end));
       dst = std::copy_n(_current, to_read, dst);
       _current += to_read;
       return {dst, to_read};
     }

     // Optional, but required to model codecs::sized_input_source
     mgs::ssize_t max_remaining_size() { return _end - _current; }

    private:
     char const* _current;
     char const* _end;
   };

Write an input range (optional)
-------------------------------

Input ranges allow iterating over input.

*mgs* provides a building block to easily create one from an input source:

.. code-block:: cpp

   #include <algorithm>
   #include <iostream>
   #include <string>

   #include <mgs/codecs/basic_input_range.hpp>
   #include <mgs/ssize_t.hpp>

   using namespace mgs;

   class noop_encoder { /* ... */ };

   int main() {
     std::string hello("Hello, World!");

     using noop_encoding_range = codecs::basic_input_range<noop_encoder>;

     noop_encoder encoder(hello.c_str(), hello.c_str() + hello.size());
     noop_encoding_range encoding_range(encoder);

     std::string hello2(encoding_range.begin(), encoding_range.end());
     // "Hello, World!"
     std::cout << hello2 << std::endl;
   }

:ref:`basic_input_range` takes a :ref:`input_source` and models :ref:`input_range`.

Define the codec traits
-----------------------

Now that we have our encoder, we can **almost** create our codec.

We still have to write a small codec traits type, which will be used by the next building block.

This type must model :ref:`codec_traits` and define:

* default types returned by **encode** and **decode** functions.
* **make_encoder** and **make_decoder** functions, taking a :ref:`input_source`

For simplicity, it will only work with :ref:`codecs::iterator_sentinel_source\<char const*> <iterator_sentinel_source>`, which is the most basic :ref:`input_source` provided by *mgs* (it just wraps an iterator/sentinel pair).

.. code-block:: cpp

   #include <mgs/codecs/iterator_sentinel_source.hpp>

   using namespace mgs;

   struct noop_codec_traits {
     using default_encoded_output = std::string;
     using default_decoded_output = default_encoded_output;

     static noop_encoder make_encoder(
         codecs::iterator_sentinel_source<char const*> is) {
       return noop_encoder(is.begin(), is.end());
     }

     static noop_encoder make_decoder(
         codecs::iterator_sentinel_source<char const*> is) {
       return noop_encoder(is.begin(), is.end());
     }
   };

Use your codec
--------------

Here we are, the last step!

We will use :ref:`basic_codec`, a helper class that needs a :ref:`codec_traits` as its template parameter, and models :ref:`codec`.

.. code-block:: cpp

   #include <mgs/codecs/basic_codec.hpp>

   using namespace mgs;

   using noop_codec = codecs::basic_codec<noop_codec_traits>;

Congratulations, you can now use your no-op codec!

Here is the full code:

.. code-block:: cpp

   #include <algorithm>
   #include <iostream>
   #include <string>
   #include <utility>

   #include <mgs/codecs/basic_codec.hpp>
   #include <mgs/codecs/basic_input_range.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>
   #include <mgs/ssize_t.hpp>

   using namespace mgs;

   class noop_encoder {
    public:
     using element_type = char;

     noop_encoder(char const* begin, char const* end)
         : _current(begin), _end(end) {}

     template <typename O>
     std::pair<O, int> read(O dst, int max_length) {
       auto const to_read =
           std::min<int>(max_length, std::distance(_current, _end));
       dst = std::copy_n(_current, to_read, dst);
       _current += to_read;
       return {dst, to_read};
     }

     // Optional, but required to model codecs::sized_input_source
     mgs::ssize_t max_remaining_size() { return _end - _current; }

    private:
     char const* _current;
     char const* _end;
   };

   struct noop_codec_traits {
     using default_encoded_output = std::string;
     using default_decoded_output = default_encoded_output;

     static noop_encoder make_encoder(
         codecs::iterator_sentinel_source<char const*> is) {
       return noop_encoder(is.begin(), is.end());
     }

     static noop_encoder make_decoder(
         codecs::iterator_sentinel_source<char const*> is) {
       return noop_encoder(is.begin(), is.end());
     }
   };

   using noop_codec = codecs::basic_codec<noop_codec_traits>;

   int main() {
     auto const s = noop_codec::encode("Hello, World!");
     auto const s2 = noop_codec::decode<std::vector<unsigned char>>(
         s.c_str(), s.c_str() + s.size());
     std::cout << s << std::endl;
   }
