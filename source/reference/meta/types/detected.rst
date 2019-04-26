.. _is_detected:

****************************************
meta::is_detected,detected_t,detected_or
****************************************

Defined in header ``<mgs/meta/detected.hpp>``.

.. code-block:: cpp

   template <template <typename...> class Op, typename... Args>
   using is_detected = /* implementation-defined */;

   template <template <typename...> class Op, typename... Args>
   using detected_t = /* implementation-defined */;

   template <typename Default, template <typename...> class Op, typename... Args>
   using detected_or = /* implementation-defined */;

   struct nonesuch {
     ~nonesuch() = delete;
     nonesuch(nonesuch const&) = delete;
     void operator=(nonesuch const&) = delete;
   };

Implementation of the :cpp:`detected idiom <experimental/is_detected>`, present in the :github:`Library Fundamentals TS v2 <cplusplus/fundamentals-ts/tree/v2>`.
