cmake_minimum_required(VERSION 3.1)
project(hidapi C)

find_package(PkgConfig)
pkg_check_modules(libusb-1.0 REQUIRED libusb-1.0)


include_directories(
     hidapi
     ${libusb-1.0_INCLUDE_DIRS}
)



set(SOURCE_FILES
        libusb/hid.c
        hidapi/hidapi.h
)

set( PUBLIC_HEADERS hidapi/hidapi.h)

add_library(hidapi SHARED ${SOURCE_FILES})
target_link_libraries(hidapi usb)


install(TARGETS hidapi 
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )
  
install(FILES ${PUBLIC_HEADERS} 
        DESTINATION include/hidapi)
