cmake_minimum_required(VERSION 3.5)

project(RCCar LANGUAGES CXX C)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

find_package(Qt5 COMPONENTS Core Network SerialPort REQUIRED)
find_package(MAVSDK REQUIRED)

add_executable(RCCar_minimal
    main.cpp
    WayWise/core/simplewatchdog.cpp
    WayWise/vehicles/objectstate.cpp
    WayWise/vehicles/carstate.cpp
    WayWise/core/vbytearray.cpp
    WayWise/vehicles/controller/motorcontroller.h
    WayWise/vehicles/controller/movementcontroller.cpp
    WayWise/vehicles/controller/servocontroller.cpp
    WayWise/vehicles/vehiclestate.cpp
    WayWise/core/pospoint.cpp
    WayWise/vehicles/controller/carmovementcontroller.cpp
    WayWise/sensors/gnss/ublox.cpp
    WayWise/sensors/gnss/rtcm3_simple.cpp
    WayWise/sensors/gnss/ubloxrover.cpp
    WayWise/sensors/camera/gimbal.h
    WayWise/communication/vehicleconnections/vehicleconnection.cpp
    WayWise/autopilot/waypointfollower.h
    WayWise/autopilot/purepursuitwaypointfollower.cpp
    WayWise/communication/mavsdkvehicleserver.cpp
)

target_include_directories(RCCar_minimal PRIVATE WayWise/)

target_link_libraries(RCCar_minimal
    PRIVATE Qt5::Network
    PRIVATE Qt5::SerialPort
    PRIVATE MAVSDK::mavsdk
)