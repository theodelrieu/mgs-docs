.. _writable:

**************
meta::writable
**************

Defined in header ``<mgs/meta/concepts/writable.hpp>``.

.. code-block:: cpp

   template <typename Out, typename T>
   concept writable =
     requires(Out&& o, T&& t) {
       *o = std::forward<T>(t);
       *std::forward<Out>(o) = std::forward<T>(t);
       const_cast<meta::iter_reference_t<Out> const&&>(*o) = std::forward<T>(t);
       const_cast<meta::iter_reference_t<Out> const&&>(*std::forward<Out>(o)) = std::forward<T>(t);
     };

Pre-C++20 implementation of the :iterconcept:`writable` concept.

----

This concept's definition is really obscure. It deserves a more detailed explanation.

The last two requirements ensure that **Out**'s **operator*** does not return a prvalue, since writing to a temporary value is unlikely to be the intended behavior (except when **Out** is a proxy-type, e.g. `std::vector<bool>::reference <https://en.cppreference.com/w/cpp/container/vector_bool/reference>`_).

Casting the result of ``*o`` to ``std::iter_reference_t<Out> const&&`` does not have any effect if the result is a reference type (including rvalue references), due to `reference collapsing <https://en.cppreference.com/w/cpp/language/reference>`_.

But if a prvalue is returned, the result will be cast to a const rvalue reference. From there, that result type's **operator=** must be a const member-function and overloaded on rvalue references.

If that is not the case, **Out** is not **writable**.

.. note::

   Although `std::vector<bool>::reference <https://en.cppreference.com/w/cpp/container/vector_bool/reference>`_ is a proxy-type, it does not model :iterconcept:`writable`, because its **operator=** is not const.

Concept emulation
=================

.. code-block:: cpp

   namespace mgs {
   namespace meta {

   template <typename Out, typename T>
   struct is_writable { /* ... */ };

   template <typename Out, typename T>
   constexpr auto is_writable_v = is_writable<In>::value;

   template <typename Out, typename T,
             typename = std::enable_if_t<is_writable_v<Out, T>>>
   using writable = Out;

   } // namespace meta
   } // namespace mgs

Example
=======

.. code-block:: cpp

   #include <mgs/meta/concepts/writable.hpp>

   struct It {
     struct Proxy {
       Proxy operator*() const;

       Proxy& operator=(std::string const&&) const;
       Proxy& operator=(std::string&&) const;
       Proxy& operator=(std::string const&) const;
       Proxy& operator=(std::string&) const;

       Proxy& operator=(Proxy const&) = default;
       Proxy& operator=(Proxy&&) = default;

       operator std::string() const;

       // Imagine having a std::string* as member
     };

     using value_type = std::string;
     using pointer = Proxy*;
     using reference = Proxy;
     using difference_type = std::ptrdiff_t;
     using iterator_category = std::input_iterator_tag;

     reference operator*();
     It& operator++();
     It operator++(int);
   };

   static_assert(is_writable<char*, char>::value, "");
   static_assert(!is_writable<char const*, char>::value, "");

   static_assert(is_writable<It, std::string>::value, "");

See also
========

* :ref:`iter_reference_t`
