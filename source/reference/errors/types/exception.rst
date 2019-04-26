*****************
errors::exception
*****************

Defined in header ``<mgs/errors/exception.hpp>``.

.. code-block:: cpp

   class exception;

Base class for all exceptions defined by *mgs*.

* :doc:`decode_error <decode_error>`

   * :doc:`unexpected_eof <unexpected_eof>`
   * :doc:`invalid_input <invalid_input>`

----

Inherited from :cpp:`std::runtime_error <error/runtime_error>`
==============================================================

Member functions
----------------

.. table:: 
   :align: left

   ========================================== ================================
   :cpp:`(constructor) <error/runtime_error>` Constructs the exception object.
   ========================================== ================================

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
