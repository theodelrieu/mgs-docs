*********
Reference
*********

.. toctree::
   :hidden:
   :titlesonly:

   base64
   base64url, base64url_nopad <base64url>
   base32
   base32hex
   base16
   base_n/types/basic_codec
   base_n/types/basic_codec_traits
   base_n/types/encode_algorithm
   base_n/types/decode_algorithm
   base_n/types/padding_policy
   base_n/concepts/encoding_traits
   codecs/types/basic_codec
   codecs/types/output_traits
   codecs/types/basic_input_range
   codecs/types/iterator_sentinel_source
   codecs/concepts/byte_type
   codecs/concepts/codec_output
   codecs/concepts/codec_traits
   codecs/concepts/codec
   codecs/concepts/input_source
   codecs/concepts/sized_input_source
   meta/types/common_reference
   meta/types/detected
   meta/types/incrementable_traits
   meta/types/iter_concept
   meta/types/iter_difference_t
   meta/types/iter_reference_t
   meta/types/iter_rvalue_reference_t
   meta/types/iter_traits
   meta/types/iter_value_t
   meta/types/iterator_t
   meta/types/iterator_traits
   meta/types/priority_tag
   meta/types/range_difference_t
   meta/types/range_reference_t
   meta/types/range_rvalue_reference_t
   meta/types/range_value_t
   meta/types/readable_traits
   meta/types/sentinel_t
   meta/types/void_t
   meta/concepts/assignable_from
   meta/concepts/bidirectional_iterator
   meta/concepts/bidirectional_range
   meta/concepts/boolean
   meta/concepts/common_range
   meta/concepts/common_reference_with
   meta/concepts/complete_type
   meta/concepts/constructible_from
   meta/concepts/convertible_to
   meta/concepts/copy_constructible
   meta/concepts/copyable
   meta/concepts/default_constructible
   meta/concepts/dereferenceable
   meta/concepts/derived_from
   meta/concepts/destructible
   meta/concepts/equality_comparable
   meta/concepts/equality_comparable_with
   meta/concepts/forward_iterator
   meta/concepts/forward_range
   meta/concepts/incrementable
   meta/concepts/input_iterator
   meta/concepts/input_range
   meta/concepts/integral
   meta/concepts/input_or_output_iterator
   meta/concepts/movable
   meta/concepts/move_constructible
   meta/concepts/output_iterator
   meta/concepts/output_range
   meta/concepts/random_access_iterator
   meta/concepts/random_access_range
   meta/concepts/range
   meta/concepts/readable
   meta/concepts/regular
   meta/concepts/same_as
   meta/concepts/semiregular
   meta/concepts/sentinel_for
   meta/concepts/signed_integral
   meta/concepts/sized_sentinel_for
   meta/concepts/swappable
   meta/concepts/totally_ordered
   meta/concepts/totally_ordered_with
   meta/concepts/weakly_equality_comparable_with
   meta/concepts/weakly_incrementable
   meta/concepts/writable
   errors/types/exception
   errors/types/decode_error
   errors/types/unexpected_eof
   errors/types/invalid_input
   config/types/ssize_t

.. table::
   :align: left

   +----------------+------------------------------------------------+--------------------------------------------------------+
   | Module         | Types                                          | Concepts                                               |
   +================+================================================+========================================================+
   | base64         | :doc:`base64`                                  |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | base64url      | | :doc:`base64url`                             |                                                        |
   |                | | :doc:`base64url_nopad <base64url>`           |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | base32         | :doc:`base32`                                  |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | base32hex      | :doc:`base32hex`                               |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | base16         | :doc:`base16`                                  |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | base_n         | | :doc:`base_n/types/basic_codec`              | :doc:`base_n/concepts/encoding_traits`                 |
   |                | | :doc:`base_n/types/encode_algorithm`         |                                                        |
   |                | | :doc:`base_n/types/decode_algorithm`         |                                                        |
   |                | | :doc:`base_n/types/padding_policy`           |                                                        |
   |                | | :doc:`base_n/types/basic_codec_traits`       |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | codecs         | | :doc:`codecs/types/basic_codec`              | | :doc:`codecs/concepts/byte_type`                     |
   |                | | :doc:`codecs/types/output_traits`            | | :doc:`codecs/concepts/codec_output`                  |
   |                | | :doc:`codecs/types/basic_input_range`        | | :doc:`codecs/concepts/codec_traits`                  |
   |                | | :doc:`codecs/types/iterator_sentinel_source` | | :doc:`codecs/concepts/codec`                         |
   |                |                                                | | :doc:`codecs/concepts/input_source`                  |
   |                |                                                | | :doc:`codecs/concepts/sized_input_source`            |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | meta           | | :doc:`meta/types/common_reference`           | | :doc:`meta/concepts/assignable_from`                 |
   |                | | :doc:`meta/types/detected`                   | | :doc:`meta/concepts/bidirectional_iterator`          |
   |                | | :doc:`meta/types/incrementable_traits`       | | :doc:`meta/concepts/bidirectional_range`             |
   |                | | :doc:`meta/types/iter_concept`               | | :doc:`meta/concepts/boolean`                         |
   |                | | :doc:`meta/types/iter_difference_t`          | | :doc:`meta/concepts/common_range`                    |
   |                | | :doc:`meta/types/iter_reference_t`           | | :doc:`meta/concepts/common_reference_with`           |
   |                | | :doc:`meta/types/iter_rvalue_reference_t`    | | :doc:`meta/concepts/complete_type`                   |
   |                | | :doc:`meta/types/iter_traits`                | | :doc:`meta/concepts/constructible_from`              |
   |                | | :doc:`meta/types/iter_value_t`               | | :doc:`meta/concepts/convertible_to`                  |
   |                | | :doc:`meta/types/iterator_t`                 | | :doc:`meta/concepts/copy_constructible`              |
   |                | | :doc:`meta/types/iterator_traits`            | | :doc:`meta/concepts/copyable`                        |
   |                | | :doc:`meta/types/priority_tag`               | | :doc:`meta/concepts/default_constructible`           |
   |                | | :doc:`meta/types/range_difference_t`         | | :doc:`meta/concepts/dereferenceable`                 |
   |                | | :doc:`meta/types/range_reference_t`          | | :doc:`meta/concepts/derived_from`                    |
   |                | | :doc:`meta/types/range_rvalue_reference_t`   | | :doc:`meta/concepts/destructible`                    |
   |                | | :doc:`meta/types/readable_traits`            | | :doc:`meta/concepts/equality_comparable`             |
   |                | | :doc:`meta/types/sentinel_t`                 | | :doc:`meta/concepts/equality_comparable_with`        |
   |                | | :doc:`meta/types/void_t`                     | | :doc:`meta/concepts/forward_iterator`                |
   |                |                                                | | :doc:`meta/concepts/forward_range`                   |
   |                |                                                | | :doc:`meta/concepts/incrementable`                   |
   |                |                                                | | :doc:`meta/concepts/input_iterator`                  |
   |                |                                                | | :doc:`meta/concepts/input_range`                     |
   |                |                                                | | :doc:`meta/concepts/integral`                        |
   |                |                                                | | :doc:`meta/concepts/input_or_output_iterator`        |
   |                |                                                | | :doc:`meta/concepts/movable`                         |
   |                |                                                | | :doc:`meta/concepts/move_constructible`              |
   |                |                                                | | :doc:`meta/concepts/output_iterator`                 |
   |                |                                                | | :doc:`meta/concepts/output_range`                    |
   |                |                                                | | :doc:`meta/concepts/random_access_iterator`          |
   |                |                                                | | :doc:`meta/concepts/random_access_range`             |
   |                |                                                | | :doc:`meta/concepts/range`                           |
   |                |                                                | | :doc:`meta/concepts/readable`                        |
   |                |                                                | | :doc:`meta/concepts/regular`                         |
   |                |                                                | | :doc:`meta/concepts/same_as`                         |
   |                |                                                | | :doc:`meta/concepts/semiregular`                     |
   |                |                                                | | :doc:`meta/concepts/sentinel_for`                    |
   |                |                                                | | :doc:`meta/concepts/signed_integral`                 |
   |                |                                                | | :doc:`meta/concepts/sized_sentinel_for`              |
   |                |                                                | | :doc:`meta/concepts/swappable`                       |
   |                |                                                | | :doc:`meta/concepts/totally_ordered`                 |
   |                |                                                | | :doc:`meta/concepts/totally_ordered_with`            |
   |                |                                                | | :doc:`meta/concepts/weakly_equality_comparable_with` |
   |                |                                                | | :doc:`meta/concepts/weakly_incrementable`            |
   |                |                                                | | :doc:`meta/concepts/writable`                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | errors         | | :doc:`errors/types/exception`                |                                                        |
   |                | | :doc:`errors/types/decode_error`             |                                                        |
   |                | | :doc:`errors/types/unexpected_eof`           |                                                        |
   |                | | :doc:`errors/types/invalid_input`            |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
   | config         | :doc:`config/types/ssize_t`                    |                                                        |
   +----------------+------------------------------------------------+--------------------------------------------------------+
