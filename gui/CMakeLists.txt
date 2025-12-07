
add_library(qlonglongspinbox SHARED qlonglongspinbox.cpp)

target_include_directories(qlonglongspinbox PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/gui)

find_package(Qt6 COMPONENTS Widgets REQUIRED)
target_link_libraries(qlonglongspinbox PRIVATE Qt6::Widgets)

target_compile_definitions(qlonglongspinbox PUBLIC  QLONGLONGSPINBOX_LIBRARY)

set_target_properties(qlonglongspinbox PROPERTIES AUTOMOC ON)

target_sources(qlonglongspinbox PRIVATE gui/qlonglongspinbox.h)


otr_module(user-interface BIN)

target_link_libraries(${self} PRIVATE
    opentrack-migration
    opentrack-logic
    opentrack-input
    opentrack-spline
    opentrack-pose-widget
    qlonglongspinbox
)

if(NOT APPLE AND NOT WIN32)
    target_compile_definitions(${self} PRIVATE -DOTR_X11_THREADS)
    otr_pkgconfig(${self} x11)
endif()
