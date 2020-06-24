**********************
errors::unexpected_eof
**********************

Defined in header ``<mgs/errors/unexpected_eof.hpp>``.

.. code-block:: cpp

   class unexpected_eof;

Defines a type of object to be thrown as an exception. It reports errors happening when end of input was reached before decoding ended.

Inherits from :doc:`decode_error <decode_error>`.

----

Inherited from :cpp:`std::runtime_error <error/runtime_error>`
==============================================================

Constructors
------------

.. code-block:: cpp

   explicit unexpected_eof(std::string const& what_arg); // 1
   explicit unexpected_eof(char const* what_arg);        // 2 

Constructs the exception object with *what_arg* as explanatory string that can be accessed through :cpp:`what() <error/exception/what>`.

Parameters
^^^^^^^^^^

**what_arg** -- explanatory string

Exceptions
^^^^^^^^^^

May throw :cpp:`std::bad_alloc <memory/new/bad_alloc>`.


Inherited from :cpp:`std::exception <error/exception>`
======================================================

Member functions
----------------

.. table::
   :align: left

   ========================================================== =============================
   :cpp:`(destructor) [virtual] <error/exception/~exception>` Destroys the exception object
   :cpp:`what [virtual] <error/exception/what>`               Returns an explanatory string
   ========================================================== =============================
