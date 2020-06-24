.. _ssize_t:

************
mgs::ssize_t
************

Defined in header ``<mgs/config/ssize_t.hpp>``.

.. code-block:: cpp

   using ssize_t =
       std::common_type_t<std::ptrdiff_t, std::make_signed_t<std::size_t>>;

Signed integral type representing indices and sizes in *mgs*.
