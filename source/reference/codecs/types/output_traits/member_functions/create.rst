*****************************
codecs::output_traits::create
*****************************

.. code-block:: cpp

   template <meta::input_range R>
   static output_type create(R& rng);

Returns an :ref:`output_type` value filled with ``rng`` 's content.

.. note::

   For a list of supported return types, look :ref:`here <supported-return-types>`.

----

Parameters
==========

* **rng** - Range from which to read content, must model :ref:`input_range`.

Return value
============

A :ref:`output_type` value, filled with ``rng`` 's content.

Example
=======

.. code-block:: cpp

   #include <mgs/base64.hpp>
   #include <mgs/codecs/output_traits.hpp>

   using namespace mgs;
   using namespace mgs::codecs;

   int main() {
      using input_source_t = iterator_sentinel_source<std::string::iterator>;

      std::string hello("Hello, World!");
      input_source_t input_source(hello.begin(), hello.end());
      auto encoder = base64::make_encoder(input_source);

      auto v = output_traits<std::vector<char>>::create(encoder);
   }
