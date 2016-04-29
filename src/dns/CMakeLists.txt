
re_module_add(client.c cstr.c dname.c hdr.c ns.c rr.c rrlist.c)

if(NOT HAVE_LIBRESOLV)
	re_module_add(res.c)
endif()

if(WIN32)
	re_module_add(win32/srv.c)
endif()

if(APPLE)
	re_module_add(darwin/srv.c)
endif()
