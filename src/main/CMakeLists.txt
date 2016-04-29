
re_module_add(init.c main.c method.c)

if(HAVE_EPOLL)
	re_module_add(epoll.c)
endif()

if(USE_OPENSSL)
	re_module_add(openssl.c)
endif()
