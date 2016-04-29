
if(HAVE_DLFCN_H)
	re_module_add(dl.c)
endif()

if(WIN32)
	re_module_add(dll.c)
endif()
