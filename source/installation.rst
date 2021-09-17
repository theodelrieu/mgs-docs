Installation
************

Conan
=====

``mgs`` is available from the ``conan-center`` remote and can be installed like this:

.. code-block:: bash

   $ conan install mgs/0.2.0@

Manual
======

You can download releases on :github:`GitHub <theodelrieu/mgs/releases>`.

Integration
***********

CMake
=====

*CMake* config files are released to ease integration.
If you used Conan to install ``mgs``, you can use the ``cmake_find_package_multi`` generator for the same results.

.. code-block:: cmake

   cmake_minimum_required(VERSION 3.3)
   project(example)

   set(CMAKE_CXX_STANDARD 14)
   set(CMAKE_CXX_EXTENSIONS OFF)

   # not useful if installed with Conan
   list(APPEND CMAKE_PREFIX_PATH "<path/to/mgs>")

   find_package(mgs REQUIRED)

   add_executable(example main.cpp)
   target_link_libraries(example mgs::mgs)

You can also use *CMake* components:

.. code-block:: cmake

   cmake_minimum_required(VERSION 3.3)
   project(example)

   set(CMAKE_CXX_STANDARD 14)
   set(CMAKE_CXX_EXTENSIONS OFF)

   # not useful if installed with Conan
   list(APPEND CMAKE_PREFIX_PATH "<path/to/mgs>")

   find_package(mgs REQUIRED COMPONENTS base64 base64url)

   add_executable(example main.cpp)
   target_link_libraries(example mgs::base64 mgs::base64url)

Manual
======

Passing ``-isystem/path/to/mgs/include`` to your compiler invocation should be enough.
