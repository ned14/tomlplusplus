cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(tomlplusplus)
include(GNUInstallDirs)

add_library(tomlplusplus_interface INTERFACE)
target_compile_features(tomlplusplus_interface INTERFACE cxx_std_17)
target_include_directories(tomlplusplus_interface INTERFACE
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
)

foreach(header
  "include/toml++/toml.h"
  "include/toml++/toml_default_formatter.h"
  "include/toml++/toml_node.h"
  "include/toml++/toml_parser.hpp"
  "include/toml++/toml_utf8.h"
  "include/toml++/toml_array.h"
  "include/toml++/toml_default_formatter.hpp"
  "include/toml++/toml_node.hpp"
  "include/toml++/toml_preprocessor.h"
  "include/toml++/toml_utf8_generated.h"
  "include/toml++/toml_array.hpp"
  "include/toml++/toml_formatter.h"
  "include/toml++/toml_node_view.h"
  "include/toml++/toml_print_to_stream.h"
  "include/toml++/toml_utf8_streams.h"
  "include/toml++/toml_common.h"
  "include/toml++/toml_instantiations.hpp"
  "include/toml++/toml_parse_error.h"
  "include/toml++/toml_table.h"
  "include/toml++/toml_value.h"
  "include/toml++/toml_date_time.h"
  "include/toml++/toml_json_formatter.h"
  "include/toml++/toml_parser.h"
  "include/toml++/toml_table.hpp"
  "include/toml++/toml_version.h"
)
  install(FILES "${header}"
    DESTINATION "include/toml++"
  )
endforeach()
install(TARGETS tomlplusplus_interface
        EXPORT ${PROJECT_NAME}Exports
        INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
        ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
        LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
)

file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake" "include(FindPackageHandleStandardArgs)\
\nset(\${CMAKE_FIND_PACKAGE_NAME}_CONFIG \${CMAKE_CURRENT_LIST_FILE})\
\nfind_package_handle_standard_args(${PROJECT_NAME} CONFIG_MODE)\
\ninclude(\"\${CMAKE_CURRENT_LIST_DIR}/${PROJECT_NAME}Exports.cmake\")\
\n")
install(FILES
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)
install(EXPORT ${PROJECT_NAME}Exports
  NAMESPACE ${PROJECT_NAME}::
  DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)
