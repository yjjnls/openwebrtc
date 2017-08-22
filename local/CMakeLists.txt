project( openwebrtc_local-lite C)

file( GLOB _SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c )
file( GLOB _HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h )

autocmake_add_library(openwebrtc_local-lite STATIC 
                      MODULES gstreamer-1.0 
					  SOURCES ${_SOURCES} ${_HEADERS}
                     )