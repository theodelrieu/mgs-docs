.. _encoding_traits:

***********************
base_n::encoding_traits
***********************

Defined in header ``<mgs/base_n/concepts/encoding_traits.hpp>``.

.. code-block:: cpp

   #include <mgs/base_n/padding_policy.hpp>

   template <std::size_t N>
   constexpr bool is_power_of_2()
   {
     return N != 0 && ((N & (N - 1)) == 0);
   }

   template <typename T>
   concept encoding_traits =
     requires(char c) {
       { T::alphabet } -> char const[];
       { T::padding_policy } -> padding_policy;
       { T::index_of(c) } -> meta::same_as<int>;
     } &&
     (meta::convertible_to<decltype(T::padding_character), char> ||
      T::padding_policy == padding_policy::none) &&
     is_power_of_2<sizeof(T::alphabet)>();

The **encoding_traits** concept is satisfied when a type provides the encoding information required by :ref:`base_n-basic_codec`.

----

Notation
========

* **c** - value of type ``char``

Static data members
===================

Definitions
-----------

.. table::
   :align: left

   ===================== ====================== ======================================================================
   Member                Description            Type
   ===================== ====================== ======================================================================
   **alphabet**          Base alphabet          ``char[]``
   **padding_policy**    Base padding policy    :doc:`base_n::padding_policy </reference/base_n/types/padding_policy>`
   **padding_character** Base padding character ``char``
   ===================== ====================== ======================================================================

Constraints
-----------

.. table::
   :align: left

   ===================== ======================================================
   **alphabet**          Size must be a power of 2.
   **padding_policy**    Must be either ``none``, ``optional`` or ``required``.
   **padding_character** Can be omitted when ``padding_policy`` is ``none``.
   ===================== ======================================================

Valid expressions
=================

.. table::
   :align: left

   ================== ===========
   Expression         Return type
   ================== ===========
   **T::index_of(c)** ``int``
   ================== ===========

Expression semantics
====================

.. table::
   :align: left

   ================== =========================================================
   Expression         Semantics
   ================== =========================================================
   **T::index_of(c)** Returns the index of ``c`` in ``T::alphabet``, or ``-1``.
   ================== =========================================================

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace base_n {

   template <typename T>
   struct is_encoding_traits { /* ... */ };

   template <typename T>
   constexpr auto is_encoding_traits_v = is_encoding_traits<T>::value;

   template <typename T,
             typename = std::enable_if_t<is_encoding_traits_v<T>>>
   using encoding_traits = T;

   } // namespace base_n
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <iostream>

   #include <mgs/base_n/basic_codec.hpp>
   #include <mgs/base_n/concepts/encoding_traits.hpp>
   #include <mgs/base_n/padding_policy.hpp>

   using namespace mgs;

   struct binary_traits {
     // using C++17 inline variables for simplicity
     inline static char const alphabet[] = {'0', '1'};
     inline static auto const padding_policy = base_n::padding_policy::none;

     static int index_of(char c) {
       if (c == '0') return 0;
       if (c == '1') return 1;
       return -1;
     }
   };

   int main() {
     static_assert(base_n::is_encoding_traits_v<binary_traits>, "");

     using binary_codec = base_n::basic_codec<binary_traits>;
     std::cout << binary_codec::encode("Hello, World!") << std::endl;
   }

See also
========

* :ref:`convertible_to`
* :ref:`same_as`
