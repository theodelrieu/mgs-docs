.. _readable:

**************
meta::readable
**************

Defined in header ``<mgs/meta/concepts/readable.hpp>``.

.. code-block:: cpp

   template <typename In>
   concept readable =
     requires {
        typename meta::iter_value_t<In>;
        typename meta::iter_reference_t<In>;
        typename meta::iter_rvalue_reference_t<In>;
     } &&
     meta::common_reference_with<meta::iter_reference_t<In>&&, meta::iter_value_t<In>&> &&
     meta::common_reference_with<meta::iter_reference_t<In>&&, meta::iter_rvalue_reference_t<In>&&> &&
     meta::common_reference_with<meta::iter_rvalue_reference_t<In>&&, meta::iter_value_t<In> const&>;

Pre-C++20 implementation of the :iterconcept:`readable` concept.

----

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename In>
   struct is_readable { /* ... */ };

   template <typename In>
   constexpr auto is_readable_v = is_readable<In>::value;

   template <typename In,
             typename = std::enable_if_t<is_readable_v<In>>>
   using readable = In;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/readable.hpp>

   using namespace mgs::meta;

   static_assert(is_readable_v<std::string::iterator>, "");
   static_assert(is_readable_v<char const*>, "");
   static_assert(!is_readable_v<void*>, "");

See also
========

* :ref:`common_reference_with`
* :ref:`iter_value_t`
* :ref:`iter_reference_t`
* :ref:`iter_rvalue_reference_t`
