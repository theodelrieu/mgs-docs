.. _codec_output:

********************
codecs::codec_output
********************

Defined in header ``<mgs/codecs/concepts/codec_output.hpp>``

.. code-block:: cpp

   #include <mgs/codecs/output_traits_fwd.hpp>

   template <typename T, typename R>
   concept codec_output =
     meta::input_range<R> &&
     requires (R& range) {
       { codecs::output_traits<T>::create(range) } -> meta::same_as<T>;
     };

The **codec_output** concept specifies the requirements that a type must fulfill in order to be returned by a :ref:`codec`.

It relies on the customization point :ref:`output_traits`.

----

Notation
========

* **r** - a value of type ``R&``

Template arguments
==================

Definitions
-----------

.. table::
   :align: left

   ===== =============================================
   **R** Input range from which ``T`` must be created.
   ===== =============================================

Constraints
-----------

.. table::
   :align: left

   ===== ==================
   **R** :ref:`input_range`
   ===== ==================

Valid expressions
=================

.. table::
   :align: left

   =============================== ===========
   Expressions                     Return type
   =============================== ===========
   **output_traits<T>::create(r)** ``T``
   =============================== ===========

Expression semantics
====================

.. table::
   :align: left

   =============================== ================================================
   Expressions                     Semantics
   =============================== ================================================
   **output_traits<T>::create(r)** Creates and returns a ``T`` from ``r`` 's input.
   =============================== ================================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T, typename R>
   struct is_codec_output { /* ... */ };

   template <typename T, typename R>
   constexpr auto is_codec_output_v = is_codec_output<T, R>::value;

   template <typename T, typename R,
             typename = std::enable_if_t<is_codec_output_v<T, R>>>
   using codec_output = T;

   } // namespace codecs
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <algorithm>

   #include <mgs/codecs/output_traits_fwd.hpp>
   #include <mgs/codecs/concepts/codec_output.hpp>
   #include <mgs/codecs/iterator_sentinel_source.hpp>

   #include <mgs/base64.hpp>

   #include <QLinkedList>
   #include <QList>

   // add support for QLinkedList
   namespace mgs {
   namespace codecs {

   template <typename CharT>
   struct output_traits<QLinkedList<CharT>> {

     template <typename R>
     static QLinkedList<CharT> create(R& range) {
       QLinkedList<CharT> list;
       std::copy(range.begin(), range.end(), std::back_inserter(list));
       return list;
     }
   };

   } // namespace codecs
   } // namespace mgs

   using namespace mgs;
   using namespace mgs::codecs;

   int main() {
     using encoder = base64::encoder<codecs::iterator_sentinel_source<char const*>>;
     
     static_assert(is_codec_output_v<std::string, encoder>, "");
     static_assert(is_codec_output_v<QLinkedList<char>, encoder>, "");

     static_assert(!is_codec_output_v<QList<char>, encoder>, "");
   }
