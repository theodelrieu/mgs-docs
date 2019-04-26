*********************
errors::invalid_input
*********************

Defined in header ``<mgs/errors/invalid_input.hpp>``.

.. code-block:: cpp

   class invalid_input;

Defines a type of object to be thrown as an exception. It reports input errors (that is, when the input does not represent a valid encoded result).

Inherits from :doc:`decode_error <decode_error>`.

----

Inherited from :cpp:`std::runtime_error <error/runtime_error>`
==============================================================

Constructors
------------

.. code-block:: cpp

   explicit invalid_input(std::string const& what_arg); // 1
   explicit invalid_input(char const* what_arg);        // 2 

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
