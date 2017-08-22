project( tests )

set(_modues gstreamer-1.0 gstreamer-base-1.0 
			  gstreamer-video-1.0 gstreamer-audio-1.0
			  gstreamer-rtp-1.0
			  gstreamer-app-1.0
			  gstreamer-sctp-1.0
			  json-glib-1.0
			  libsoup-2.4
			  openssl )
autocmake_check_modules(this ${_modues} )

include_directories( ${this_INCLUDE_DIRECTORIES} )
link_directories( ${this_LINK_DIRECTORIES} )

macro( _add_test _name )
    set(_name owr-lite-${_name})

	add_executable (${_name} ${ARGN})
	target_link_libraries(${_name} openwebrtc-lite-${OWR_API_VERSION} openwebrtc_gst-lite ${this_LIBS})
	install(TARGETS ${_name}
			RUNTIME DESTINATION testkits/openwebrtc	)
	add_dependencies(${_name} openwebrtc-lite-${OWR_API_VERSION} openwebrtc_gst-lite )

endmacro()

_add_test( test-init test_init.c )
_add_test( test-bus test_bus.c )
_add_test( test-uri test_uri.c test_utils.c )
_add_test( test-gst-io test_gst_io.c )
_add_test( test-list-devices list_devices.c )
_add_test( test-self-view test_self_view.c test_utils.c )
_add_test( test-send-receive test_send_receive.c test_utils.c )
_add_test( test-client test_client.c )

