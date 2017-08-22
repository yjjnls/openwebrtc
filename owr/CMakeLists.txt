project(openwebrtc-lite-${OWR_API_VERSION} C)

file( GLOB _SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c )
file( GLOB _HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h )

autocmake_install_pc(NAME openwebrtc-lite-${OWR_API_VERSION}
                     DESCRIPTION "libopenwebrtc lite"
                     REQUIRES glib-2.0 gobject-2.0 gmodule-2.0 gthread-2.0 gstreamer-1.0 nice
					 LIBS openwebrtc )
#autocmake_add_library(openwebrtc-${OWR_API_VERSION} SHARED 
#                      MODULES gstreamer-1.0 gstreamer-base-1.0 gstreamer-gl-1.0 nice openssl
#					               gstreamer-video-1.0 gstreamer-audio-1.0
#								   gstreamer-rtp-1.0
#								   gstreamer-app-1.0
#								   gstreamer-sctp-1.0
#					  SOURCES ${_SOURCES} ${_HEADERS} openwebrtc.def
#                     )
set(_modules gstreamer-1.0 gstreamer-base-1.0 
             gstreamer-gl-1.0 
			 nice openssl
             gstreamer-video-1.0 gstreamer-audio-1.0
             gstreamer-rtp-1.0 gstreamer-app-1.0
			 gstreamer-sctp-1.0 )
if(UNIX)
    list(APPEND _modules libpulse libpulse-mainloop-glib)
endif()

autocmake_check_modules(this ${_modules})

include_directories( ${this_INCLUDE_DIRECTORIES} )
link_directories( ${this_LINK_DIRECTORIES} )
add_library (openwebrtc-lite-${OWR_API_VERSION} SHARED ${_SOURCES} ${_HEADERS} openwebrtc.def)
#autocmake_add_library(openwebrtc-lite-${OWR_API_VERSION} SHARED
#                      MODULES ${_modules}
#					  SOURCES ${_SOURCES} ${_HEADERS} openwebrtc.def )
target_link_libraries(openwebrtc-lite-${OWR_API_VERSION}  
          openwebrtc_transport-lite 
		  openwebrtc_local-lite
		  ${this_LIBS}
		  )

install(TARGETS openwebrtc-lite-${OWR_API_VERSION}
        LIBRARY DESTINATION lib 
        ARCHIVE DESTINATION lib
		RUNTIME DESTINATION bin
		)
		
INSTALL(FILES owr.h owr_media_source.h owr_bus.h owr_message_origin.h owr_types.h
        DESTINATION include/owr ) 