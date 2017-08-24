cmake_minimum_required( VERSION 2.8 )

project( openwebrtc )
set(VERSION 0.3.0-2)
set(OWR_API_VERSION 0.3)
include( AutoCMake )

add_definitions( -DOWR_LITE)
autocmake_pkgconfig_init()

include_directories( ${CMAKE_SOURCE_DIR}/owr )
include_directories( ${CMAKE_SOURCE_DIR}/gst )
include_directories( ${CMAKE_SOURCE_DIR}/local )
include_directories( ${CMAKE_SOURCE_DIR}/transport )
  
add_subdirectory( local  )
add_subdirectory( transport  )
add_subdirectory( gst  )
add_subdirectory( owr  ) 
add_subdirectory( tests  )
install(DIRECTORY web DESTINATION testkits/openwebrtc )
