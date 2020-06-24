Installation
############

You can download releases on :github:`GitHub <theodelrieu/mgs/releases>`.

Integration
***********

CMake
=====

*CMake* files are released to ease integration:

.. code-block:: cmake

   cmake_minimum_required(VERSION 3.3)
   project(example)

   set(CMAKE_CXX_STANDARD 14)
   set(CMAKE_CXX_EXTENSIONS OFF)

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

   list(APPEND CMAKE_PREFIX_PATH "<path/to/mgs>")

   find_package(mgs REQUIRED COMPONENTS base64 base64url)

   add_executable(example main.cpp)
   target_link_libraries(example mgs::base64 mgs::base64url)

Manual
======

Passing ``-isystem/path/to/mgs/include`` to your compiler invocation should be enough.
