.. _sentinel_for:

******************
meta::sentinel_for
******************

Defined in header ``<mgs/meta/concepts/sentinel_for.hpp>``.

.. code-block:: cpp

   template <typename S, typename I>
     concept sentinel_for =
       meta::semiregular<S> &&
       meta::input_or_output_iterator<I> &&
       meta::weakly_equality_comparable_with<S, I>

Pre-C++20 implementation of the :iterconcept:`sentinel_for` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename S, typename I>
   struct is_sentinel_for { /* ... */ };

   template <typename S, typename I>
   constexpr auto is_sentinel_for_v = is_sentinel_for<S, I>::value;

   template <typename S, typename I,
             typename = std::enable_if_t<is_sentinel_for_v<S, I>>>
   using sentinel_for = S;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/sentinel_for.hpp>

   using namespace mgs::meta;

   struct pointer_sentinel {};

   bool operator==(char*, pointer_sentinel);
   bool operator!=(char*, pointer_sentinel);

   bool operator==(pointer_sentinel, char*);
   bool operator!=(pointer_sentinel, char*);

   static_assert(is_sentinel_for_v<char*, char*>, "");
   static_assert(is_sentinel_for_v<pointer_sentinel, char*>, "");
   static_assert(!is_sentinel_for_v<pointer_sentinel, std::vector<int>::iterator>, "");

See also
========

* :ref:`semiregular`
* :ref:`input_or_output_iterator`
* :ref:`weakly_equality_comparable_with`
