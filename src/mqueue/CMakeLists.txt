
re_module_add(mqueue.c)

if(WIN32)
	re_module_add(win32/pipe.c)
endif()
