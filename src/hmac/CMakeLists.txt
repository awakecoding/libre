
re_module_add(hmac_sha1.c)

if(USE_OPENSSL)
	re_module_add(openssl/hmac.c)
elseif(USE_APPLE_COMMONCRYPTO)
	re_module_add(apple/hmac.c)
elseif()
	re_module_add(hmac.c)
endif()
