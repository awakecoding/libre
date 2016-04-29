
re_module_add(if.c net.c netstr.c rt.c sock.c sockopt.c)

if(WIN32)
	re_module_add(posix/wif.c)
endif()

if(HAVE_SYS_SYSCTL_H)
	if(HAVE_NET_ROUTE_H)
		re_module_add(bsd/brt.c)
	endif()
endif()

if(HAVE_GETIFADDRS)
	re_module_add(net/ifaddrs.c)
endif()
