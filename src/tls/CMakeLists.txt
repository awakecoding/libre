
if(USE_OPENSSL)
	re_module_add(openssl/tls.c openssl/tls_tcp.c openssl/tls_udp.c)
endif()
