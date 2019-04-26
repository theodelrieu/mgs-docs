Advanced
========

This section groups some of *mgs*' advanced quirks and tricks.

.. _supported-return-types:

Supported return types
----------------------

Here is the list of supported return types:

* :cpp:`std::array <container/array>`
* Sequence containers that are :ref:`constructible_from` a pair of input iterator/sentinel.
* Sequence containers that fulfill the following constraints:
   * :ref:`output_range`
   * :ref:`default_constructible`
   * :ref:`movable` or :ref:`copyable`
   * have a ``resize(size_type)`` member function

.. warning::

   When using :cpp:`std::array <container/array>`, an exception will be thrown if the transformed data does not fit **EXACTLY** in the array.

.. _signed_sizes:

Signed sizes
------------

Contrary to the STL, *mgs* represents sizes and offsets as signed integers.

The rationale can be found in Bjarne Stroustrup's `paper <http://open-std.org/JTC1/SC22/WG21/docs/papers/2019/p1428r0.pdf>`_.

*mgs* provides the :ref:`ssize_t` type alias, defined in ``<mgs/ssize_t.hpp>`` as followed:

.. code-block:: cpp

   using ssize_t =
       std::common_type_t<std::ptrdiff_t, std::make_signed_t<std::size_t>>;

.. note::

   :ref:`ssize_t` will be used in this documentation, to avoid confusion with the POSIX's *ssize_t*.


.. _emulated-concepts:

Emulated concepts
-----------------

As mentioned previously, *mgs* emulates C++20 concepts to properly constrain its APIs.

This subsection will explain how to use those emulated concepts.

.. note::

   If you are looking for a quick introduction to concepts, you can take a look :doc:`here </concepts_refresher>`.

Using type traits
^^^^^^^^^^^^^^^^^

*mgs* exposes a type trait and a variable template for every concept.

Here is how to constraint a function on :ref:`input_range`:

.. code-block:: cpp

   #include <iostream>
   #include <string>
   #include <type_traits>
   #include <vector>

   #include <mgs/meta/concepts/input_range.hpp>

   using namespace mgs;

   template <typename R, typename = std::enable_if_t<meta::is_input_range_v<R>>>
   void print_range(R const& range) {
     for (auto const& elem : range)
       std::cout << elem << '\n';
   }

   int main() {
     std::vector<std::string> v{"Hello", ", ", "World"};
     print_range(v);
     print_range("Hello");
   }

.. _using-type-aliases:

Using type aliases
^^^^^^^^^^^^^^^^^^

*mgs* also exposes an alias which bears the concept name.

.. code-block:: cpp

   #include <mgs/meta/concepts/input_range.hpp>

   using namespace mgs;

   template <typename R, typename = meta::input_range<R>>
   void print_range(R const&) { /* ... */ }

   // alternative
   template <typename R>
   void print_range(meta::input_range<R> const&) { /* ... */ }

This is quite handy, however there is a caveat with overloads.

Imagine we have two aliases **integral** and **signed_integral**:

.. code-block:: cpp

   template <typename T,
             typename = std::enable_if_t<std::is_integral<T>::value>>
   using integral = T;

   template <typename T,
             typename = std::enable_if_t<std::is_signed<T>::value &&
                                         std::is_integral<T>::value>>
   using signed_integral = T;

Let's try to use them:

.. code-block:: cpp

   template <typename T>
   void print_integral(signed_integral<T> i) { /* ... */ }

   template <typename T>
   void print_integral(integral<T> i) { /* ... */ }

Since those are just aliases to their first template parameter, the compiler complains that we redefined ``print_integral``, even with the :cpp:`std::enable_if <types/enable_if>` in the aliases' template parameters!

Luckily, there is a way to force overload resolution by setting a "priority" to each of them:

.. code-block:: cpp

   #include <iostream>
   #include <type_traits>

   #include <mgs/meta/priority_tag.hpp>

   using namespace mgs;

   template <typename T, typename = std::enable_if_t<std::is_integral<T>::value>>
   using integral = T;

   template <typename T, typename = std::enable_if_t<std::is_signed<T>::value &&
                                                     std::is_integral<T>::value>>
   using signed_integral = T;

   // signed_integral is more specialized than integral, hence priority_tag<1>
   template <typename T>
   void print_integral(signed_integral<T> i, meta::priority_tag<1>) {
     std::cout << "signed_integral: " << i << std::endl;
   }

   // Fallback overload
   template <typename T>
   void print_integral(integral<T> i, meta::priority_tag<0>) {
     std::cout << "integral: " << i << std::endl;
   }

   int main() {
     meta::priority_tag<1> tag;
     print_integral(2, tag);   // calls first overload
     print_integral(2u, tag);  // calls second overload
     // fails to compile
     // print_integral("", tag);
   }

Usually, you would rather have ``priority_tag`` in ``print_integral_impl`` methods, and have a top-level ``print_integral`` forwarding the call to ``print_integral_impl``.

.. note::

   This idea of template aliases comes from Arthur O'Dwyer's `blog <https://quuxplusone.github.io/blog/2018/08/23/stop-cascading-errors>`_.

Debugging concepts
^^^^^^^^^^^^^^^^^^

Figuring out why an API constraint is not fulfilled can be very hard.

Let's take the following example:

.. code-block:: cpp

   #include <cstddef>
   #include <iterator>

   #include <mgs/meta/concepts/random_access_iterator.hpp>

   using namespace mgs;

   struct iterator_fail {
     using value_type = int;
     using pointer = value_type*;
     using reference = value_type&;
     using difference_type = std::ptrdiff_t;
     using iterator_category = std::random_access_iterator_tag;

     iterator_fail& operator++();
     iterator_fail operator++(int);
     iterator_fail& operator--();
     iterator_fail operator--(int);

     iterator_fail& operator+=(difference_type);
     reference operator[](difference_type) const;
     iterator_fail operator-(difference_type) const;
     friend iterator_fail operator+(difference_type, iterator_fail);
     friend difference_type operator-(iterator_fail, iterator_fail);
     reference operator*();
   };

   bool operator==(iterator_fail, iterator_fail);
   bool operator!=(iterator_fail, iterator_fail);

   int main() {
     static_assert(meta::is_random_access_iterator_v<iterator_fail>, "");
   }

The ``static_assert`` fails, but can you figure out why the ``iterator_fail`` is not a :ref:`random_access_iterator`?

There's two ways to find out:

#. Browse the documentation for at least 15 minutes, monkey-patch the iterator until it works.
#. Use ``meta::trigger_static_asserts``.

.. code-block:: cpp

   #include <cstddef>
   #include <iterator>

   #include <mgs/meta/concepts/random_access_iterator.hpp>
   #include <mgs/meta/static_asserts.hpp>

   using namespace mgs;

   struct iterator_fail {
     using value_type = int;
     using pointer = value_type*;
     using reference = value_type&;
     using difference_type = std::ptrdiff_t;
     using iterator_category = std::random_access_iterator_tag;

     iterator_fail& operator++();
     iterator_fail operator++(int);
     iterator_fail& operator--();
     iterator_fail operator--(int);

     iterator_fail& operator+=(difference_type);
     reference operator[](difference_type) const;
     iterator_fail operator-(difference_type) const;
     friend iterator_fail operator+(difference_type, iterator_fail);
     friend difference_type operator-(iterator_fail, iterator_fail);
     reference operator*();
   };

   bool operator==(iterator_fail, iterator_fail);
   bool operator!=(iterator_fail, iterator_fail);

   int main() {
     // Note that ::value is not used!
     meta::trigger_static_asserts<meta::is_random_access_iterator<iterator_fail>>();
   }

You will get a compiler error, with several ``static_assert`` explaining what is going on.

The output you get will vary depending on your compiler, here is mine when piping GCC 8's error output into ``grep 'static assertion'``:

::

  error: static assertion failed: T does not model meta::random_access_iterator
  error: static assertion failed: invalid or missing operator: 'T operator+(T const, meta::iter_difference_t<T>)'
  error: static assertion failed: invalid or missing operator: 'T operator-=(meta::iter_difference_t<T>)'
  error: static assertion failed: T does not model meta::totally_ordered
  error: static assertion failed: invalid or missing operator: 'meta::boolean operator<(T const&, T const&)'
  error: static assertion failed: invalid or missing operator: 'meta::boolean operator<=(T const&, T const&)'
  error: static assertion failed: invalid or missing operator: 'meta::boolean operator>(T const&, T const&)'
  error: static assertion failed: invalid or missing operator: 'meta::boolean operator>=(T const&, T const&)'

Not as good as C++20 concepts, but at least the information is clearer. Let's complete (and rename) our iterator:

.. code-block:: cpp

   #include <cstddef>
   #include <iterator>

   #include <mgs/meta/concepts/random_access_iterator.hpp>

   using namespace mgs;

   struct iterator_success {
     using value_type = int;
     using pointer = value_type*;
     using reference = value_type&;
     using difference_type = std::ptrdiff_t;
     using iterator_category = std::random_access_iterator_tag;

     iterator_success& operator++();
     iterator_success operator++(int);
     iterator_success& operator--();
     iterator_success operator--(int);

     iterator_success& operator+=(difference_type);
     reference operator[](difference_type) const;
     iterator_success operator-(difference_type) const;
     friend iterator_success operator+(difference_type,
                                       iterator_success);
     friend difference_type operator-(iterator_success,
                                      iterator_success);
     reference operator*();

     // missing functions
     friend iterator_success operator+(difference_type, iterator_success);
     iterator_success& operator-=(difference_type);
   };

   bool operator==(iterator_success, iterator_success);
   bool operator!=(iterator_success, iterator_success);

   // Indeed, meta::totally_ordered is a requirement of meta::random_access_iterator
   bool operator<(iterator_success, iterator_success);
   bool operator<=(iterator_success, iterator_success);
   bool operator>(iterator_success, iterator_success);
   bool operator>=(iterator_success, iterator_success);

   int main() {
     static_assert(meta::is_random_access_iterator_v<iterator_success>, "");
   }

Now the code should compile!

.. warning::

   Do not forget to remove ``static_asserts.hpp`` from your includes, as it does a lot of heavy meta-programming tricks that will slow down your compilation.
