
if(HAVE_PTHREAD_RWLOCK)
	re_module_add(rwlock.c)
elseif(HAVE_PTHREAD)
	re_module_add(lock.c)
endif()

if(WIN32)
	re_module_add(lock.c)
endif()
