******************
Concepts refresher
******************

This section briefly introduces C++ concepts.

Motivation
==========

Concepts help constraining generic code. Taking the the following code:

.. code-block:: cpp

   template <typename T>
   auto add_numbers(T lhs, T rhs) {
     return lhs + rhs;
   }

It will work with numbers but nothing prevents passing :cpp:`std::string <string/basic_string>`, which seems odd for an ``add_numbers`` function. 

Let's constrain ``T`` to only accept integral types. We will use the :concept:`integral` concept for that matter.

.. code-block:: cpp

   template <std::integral T>
   auto add_numbers(T lhs, T rhs) {
     return lhs + rhs;
   }

Calling ``add_numbers`` with :cpp:`std::string <string/basic_string>` will now fail to compile.

Concept definition syntax
=========================

Here is a toy concept definition, which will be useful to read and understand more advanced concepts:

.. code-block:: cpp

   template <typename T>
   concept foo =
     std::default_constructible<T> &&                     // 1.
     requires(T const& value) {                           // 2.
       std::signed_integral<typename T::difference_type>; // 3.
       { value.size() } -> std::same_as<std::size_t>;     // 4.
     };

#. ``T`` must model :concept:`default_constructible`.
#. :cpp:`requires <keyword/requires>` clause allows using values of any type (here ``T const&``) to ensure the validity of expressions composing it.
#. ``T::difference_type`` must exist, and model :concept:`signed_integral`.
#. ``value.size()`` must be a valid expression, and return **exactly** :cpp:`std::size_t <types/size_t>`.

.. hint::

   When a concept is specified after ``->``, its first template parameter is omitted. It will be set automatically by the compiler.

   ``4.`` could have been written as ``std::same_as<decltype((value.size())), std::size_t>``.

.. note::

   To learn more about Concepts, take a look :cpp:`here <language/constraints>`.

Concept emulation
=================

Concepts are a C++20 feature, and thus are not used in the code.

To emulate them, *mgs* defines for each concept:

* a type trait
* a variable template
* a type alias

Taking back the *foo* toy concept from above:

.. code-block:: cpp

   namespace mgs {

   template <typename T, typename U>
   struct is_foo { /* ... */ };

   template <typename T, typename U>
   constexpr auto is_foo_v = is_foo<T, U>::value;

   template <typename T,
             typename U,
             typename = std::enable_if_t<is_foo_v<T, U>>>
   using foo = T;

   } // namespace mgs

To know more about concept emulation and how to use it, take a look :ref:`here <emulated-concepts>`.

.. important::

   Every concept emulated by mgs tries to be as SFINAE-friendly as possible. i.e. passing ``void`` to most traits will compile, whereas it would trigger undefined behavior for their ``std`` counterparts (which often means compiler errors).

   The rationale behind this difference is that the need to short-circuit SFINAE conditions (to handle types like ``void``) in generic context is a pain. And my feeling is that statements like ``std::is_base_of_v<std::string, void>`` should return ``false`` instead of yielding a compiler error.
