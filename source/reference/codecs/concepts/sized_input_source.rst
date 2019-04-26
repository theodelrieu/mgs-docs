.. _sized_input_source:

**************************
codecs::sized_input_source
**************************

Defined in header ``<mgs/codecs/concepts/sized_input_source.hpp>``

.. code-block:: cpp

   template <typename T>
   concept sized_input_source =
     codecs::input_source<T> &&
     requires(T const& cs) {
       { cv.max_remaining_size() } -> meta::convertible_to<mgs::ssize_t>;
     };

The **sized_input_source** concept is a refinement of :ref:`input_source` which can compute the maximum number of remaining bytes.

----

Notation
========

* **cs** - value of type ``T const&``

Refinements
===========

* :ref:`input_source`

Valid expressions
=================

.. table::
   :align: left

   =========================== ===========================================================
   Expression                  Return type
   =========================== ===========================================================
   **cs.max_remaining_size()** :ref:`meta::convertible_to\<mgs::ssize_t> <convertible_to>`
   =========================== ===========================================================

Expression semantics
====================

.. table::
   :align: left

   =========================== =============================================
   Expression                  Semantics
   =========================== =============================================
   **cs.max_remaining_size()** Returns the maximum number of remaining bytes
   =========================== =============================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T>
   struct is_sized_input_source { /* ... */ };

   template <typename T>
   constexpr auto is_sized_input_source_v = is_sized_input_source<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_sized_input_source_v<T>>>
   using sized_input_source = T;

   } // namespace codecs
   } // namespace mgs
   
Example
=======

.. code-block:: cpp

   #include <mgs/codecs/concepts/sized_input_source.hpp>

   using namespace mgs::codecs;

   struct vector_input_source {
     using element_type = unsigned char;

     std::vector<unsigned char> buffer;
     int pos = 0;

     vector_input_source() : buffer(4096) {}

     int read(unsigned char* dst, int n) {
       auto const to_read = std::min<int>(n, buffer.size() - pos);
       std::copy_n(buffer.begin() + pos, to_read, dst);
       pos += to_read;
       return to_read;
     }

     mgs::ssize_t max_remaining_size() const {
       return buffer.size() - pos;
     }
   };

   static_assert(is_sized_input_source_v<vector_input_source>, "");
