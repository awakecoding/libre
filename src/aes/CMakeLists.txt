
if(USE_OPENSSL)
	re_module_add(openssl/aes.c)
elseif(USE_APPLE_COMMONCRYPTO)
	re_module_add(apple/aes.c)
else()
	re_module_add(stub.c)
endif()
