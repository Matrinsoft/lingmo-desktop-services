set(SCREEN_SRCS
    common/control.cpp
    common/globals.cpp
    common/orientation_sensor.cpp
    common/utils.cpp
    confighandler.cpp
    outputmodel.cpp
    plugin.cpp
    screen.cpp
)

find_package(KF6Screen QUIET)
find_package(KF6KIO QUIET)
find_package(Qt6 REQUIRED COMPONENTS Test Sensors)
if(NOT KF6Screen_FOUND)
    message(STATUS "KF6Screen not found, skipping screen plugin")
    return()
endif()

add_library(lingmoscreen_qmlplugins SHARED ${SCREEN_SRCS})

target_link_libraries(lingmoscreen_qmlplugins
    Qt6::Core
    Qt6::Quick
    Qt6::Gui
    Qt6::DBus
    Qt6::Sensors
    Qt6::Test

    KF6::Screen
    KF6::KIOCore
)

install(TARGETS lingmoscreen_qmlplugins DESTINATION ${INSTALL_QMLDIR}/Lingmo/Screen)
install(FILES qmldir DESTINATION ${INSTALL_QMLDIR}/Lingmo/Screen)
