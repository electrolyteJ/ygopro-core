project (ocgcore)

file(GLOB_RECURSE AUTO_FILES_RESULT
    "*.cpp"
    "*.c"
    "*.h"
)

if (MSVC)
    include_directories ( ../lua )
else ()
    include_directories ( ${LUA_INCLUDE_DIR} )
endif ()

add_library (ocgcore SHARED ${AUTO_FILES_RESULT})
include(GenerateExportHeader)
generate_export_header(ocgcore
    BASE_NAME ocgcore
    EXPORT_MACRO_NAME OCGCORE_API
    EXPORT_FILE_NAME ocgcore_export.h
)

target_include_directories(ocgcore PUBLIC
    ${CMAKE_CURRENT_BINARY_DIR}
)

if (MSVC)
    target_link_libraries (ocgcore lua)
else ()
    target_link_libraries (ocgcore ${LUA_LIBRARIES})
endif ()
