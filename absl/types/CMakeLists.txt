#
# Copyright 2017 The Abseil Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

list(APPEND TYPES_PUBLIC_HEADERS
  "any.h"
  "bad_any_cast.h"
  "bad_optional_access.h"
  "optional.h"
  "span.h"
)



list(APPEND BAD_ANY_CAST_SRC
    "bad_any_cast.cc"
    ${TYPES_PUBLIC_HEADERS}
)
set(BAD_ANY_CAST_PUBLIC_LIBRARIES base)

abseil_library(
  TARGET
      bad_any_cast
  SOURCES
      ${BAD_ANY_CAST_SRC}
  PUBLIC_LIBRARIES
      ${BAD_ANY_CAST_PUBLIC_LIBRARIES}
)



set(OPTIONAL_SRC "optional.cc")
set(OPTIONAL_PUBLIC_LIBRARIES base)

abseil_library(
  TARGET
      optional
  SOURCES
      ${OPTIONAL_SRC}
  PUBLIC_LIBRARIES
      ${OPTIONAL_PUBLIC_LIBRARIES}
)


set(BAD_OPTIONAL_ACCESS_SRC "bad_optional_access.cc")
set(BAD_OPTIONAL_ACCESS_LIBRARIES base)

abseil_library(
  TARGET
      bad_optional_access
  SOURCES
      ${BAD_OPTIONAL_ACCESS_SRC}
  PUBLIC_LIBRARIES
      ${BAD_OPTIONAL_ACCESS_PUBLIC_LIBRARIES}
)

install(FILES ${TYPES_PUBLIC_HEADERS}
        DESTINATION ${CMAKE_INSTALL_FULL_INCLUDEDIR}/absl/types)


#
## TESTS
#


# test any_test
set(ANY_TEST_SRC "any_test.cc")
set(ANY_TEST_PUBLIC_LIBRARIES base throw_delegate bad_any_cast test_instance_tracker_lib)

abseil_test(
  TARGET
      any_test
  SOURCES
      ${ANY_TEST_SRC}
  PUBLIC_LIBRARIES
      ${ANY_TEST_PUBLIC_LIBRARIES}
  PRIVATE_COMPILE_FLAGS
      ${ABSL_EXCEPTIONS_FLAG}
)


# test any_test_noexceptions
abseil_test(
  TARGET
      any_test_noexceptions
  SOURCES
      ${ANY_TEST_SRC}
  PUBLIC_LIBRARIES
      ${ANY_TEST_PUBLIC_LIBRARIES}
)


# test span_test
set(SPAN_TEST_SRC "span_test.cc")
set(SPAN_TEST_PUBLIC_LIBRARIES base strings throw_delegate bad_any_cast test_instance_tracker_lib)

abseil_test(
  TARGET
      span_test
  SOURCES
      ${SPAN_TEST_SRC}
  PUBLIC_LIBRARIES
      ${SPAN_TEST_PUBLIC_LIBRARIES}
  PRIVATE_COMPILE_FLAGS
      ${ABSL_EXCEPTIONS_FLAG}
)


# test span_test_noexceptions
abseil_test(
  TARGET
      span_test_noexceptions
  SOURCES
      ${SPAN_TEST_SRC}
  PUBLIC_LIBRARIES
      ${SPAN_TEST_PUBLIC_LIBRARIES}
)



# test optional_test
set(OPTIONAL_TEST_SRC "optional_test.cc")
set(OPTIONAL_TEST_PUBLIC_LIBRARIES base throw_delegate optional bad_optional_access)

abseil_test(
  TARGET
      optional_test
  SOURCES
      ${OPTIONAL_TEST_SRC}
  PUBLIC_LIBRARIES
      ${OPTIONAL_TEST_PUBLIC_LIBRARIES}
)


