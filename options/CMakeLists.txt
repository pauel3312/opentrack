otr_module(options NO-COMPAT BIN)
if(NOT WIN32 AND NOT APPLE)
    target_link_libraries(opentrack-options PRIVATE rt)
elseif(WIN32)
    target_compile_definitions(opentrack-options PRIVATE OPENTRACK_COMPAT_STATIC)
endif()

target_link_libraries(opentrack-options PRIVATE opentrack-compat)
