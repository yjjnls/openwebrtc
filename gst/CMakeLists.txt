project(openwebrtc_gst-lite C)

file( GLOB _SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c )
file( GLOB _HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h )

autocmake_install_pc(NAME openwebrtc-gst-lite-${OWR_API_VERSION}
                     DESCRIPTION "libopenwebrtc-gst-lite"
                     REQUIRES gstreamer-1.0 openwebrtc-lite-0.3
					 LIBS openwebrtc_gst )
					 
autocmake_add_library(openwebrtc_gst-lite SHARED 
                      MODULES gstreamer-1.0 gstreamer-video-1.0
					  SOURCES ${_SOURCES} ${_HEADERS} openwebrtc-gst.def )
#openwebrtc_transport openwebrtc_local 
target_link_libraries(openwebrtc_gst-lite openwebrtc-lite-${OWR_API_VERSION} )		
install(TARGETS openwebrtc_gst-lite
        LIBRARY DESTINATION lib 
        ARCHIVE DESTINATION lib
		RUNTIME DESTINATION bin
		)					  
INSTALL(FILES owr_gst_audio_renderer.h owr_gst_media_source.h owr_gst_video_renderer.h
        DESTINATION include/owr )				 
add_dependencies(openwebrtc_gst-lite openwebrtc-lite-${OWR_API_VERSION} )
    
