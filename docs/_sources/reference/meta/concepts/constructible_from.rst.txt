.. _constructible_from:

************************
meta::constructible_from
************************

Defined in header ``<mgs/meta/concepts/constructible_from.hpp>``.

.. code-block:: cpp

   template <typename T, typename... Args>
   concept constructible_from =
     meta::destructible<T> &&
     std::is_constructible_v<T, Args...>;

Pre-C++20 implementation of the :concept:`constructible_from` concept.

----

Differences with the C++20 version
==================================

* Checks template arguments before calling :cpp:`std::is_constructible_v <types/is_constructible>`, which is not SFINAE-friendly.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename T, typename... Args>
   struct is_constructible_from { /* ... */ };

   template <typename T, typename... Args>
   constexpr auto is_constructible_from_v = is_constructible_from<T, Args...>::value;

   } // namespace meta
   } // namespace mgs

.. note::

   Unlike other concept emulations, there is no ``constructible_from`` alias because of the template parameter pack.

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/constructible_from.hpp>

   using namespace mgs::meta;

   static_assert(is_constructible_from_v<int>, "");
   static_assert(is_constructible_from_v<std::string, std::string const&>, "");
   static_assert(is_constructible_from_v<std::string, int, int, int, int>, "");
   static_assert(!is_constructible_from_v<int, void>, "");

See also
========

* :ref:`destructible`
