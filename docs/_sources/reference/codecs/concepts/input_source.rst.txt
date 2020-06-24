.. _input_source:

********************
codecs::input_source
********************

Defined in header ``<mgs/codecs/concepts/input_source.hpp>``.

.. code-block:: cpp

   template <typename T, typename O = typename T::element_type*>
   concept input_source =
     meta::movable<T> &&
     requires(T& is, O dst, mgs::ssize_t n)
       meta::default_constructible<typename T::element_type>;
       meta::output_iterator<O, typename T::element_type>;
       { is.read(dst, n) } -> std::pair<O, meta::convertible_to<mgs::ssize_t>>;
     };

The **input_source** concept specifies that a type provides sequenced reads of input into a :ref:`output_iterator`.

----

Notation
========

* **is** - value of type ``T&``
* **dst** - value of type ``O``
* **n** - value of type :ref:`ssize_t`

Constraints
===========

* :ref:`movable`

Template arguments
==================

Definitions
-----------

.. table::
   :align: left

   ===== =============================================
   **O** Iterator to be filled with the source's input
   ===== =============================================

Constraints
-----------

.. table::
   :align: left

   ===== =========================================================================
   **O** :ref:`meta::output_iterator\<typename T::element_type> <output_iterator>`
   ===== =========================================================================

Member types
============

Definitions
-----------

.. table::
   :align: left

   ================ =====================================================
   **element_type** The type of elements which will be written in ``dst``
   ================ =====================================================

Constraints
-----------

.. table::
   :align: left

   ================ ============================
   **element_type** :ref:`default_constructible`
   ================ ============================

Valid expressions
=================

.. table::
   :align: left

   =================== ==========================================================================
   Expression          Return type
   =================== ==========================================================================
   **is.read(dst, n)** :ref:`std::pair\<O, meta::convertible_to\<mgs::ssize_t>> <convertible_to>`
   =================== ==========================================================================

Expression semantics
====================

.. table::
   :align: left

   =================== ==================================================================
   Expression          Semantics
   =================== ==================================================================
   **is.read(dst, n)** | Reads at most ``n`` bytes of input into ``dst``.
                       | Returns a pair containing:
                       | * an iterator which should be given to subsequent ``read`` calls
                       | * the number of bytes written, ``0`` being EOF.
   =================== ==================================================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace codecs {

   template <typename T, typename O = typename T::element_type*>
   struct is_input_source { /* ... */ };

   template <typename T, typename O = typename T::element_type*>
   constexpr auto is_input_source_v = is_input_source<T, O>::value;

   template <typename T,
             typename O = typename T::element_type*,
             typename = std::enable_if_t<is_input_source<T, O>>>
   using input_source = T;

   } // namespace codecs
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <algorithm>
   #include <vector>

   #include <mgs/codecs/concepts/input_source.hpp>

   using namespace mgs;
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
   };

   static_assert(is_input_source_v<vector_input_source>, "");

See also
========

* :ref:`convertible_to`
* :ref:`movable`
* :ref:`output_iterator`
* :ref:`ssize_t`
