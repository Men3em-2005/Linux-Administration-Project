# Caesar static library
add_library(caesar STATIC
    caesar_cipher/src/caesar_encrypt.c
    caesar_cipher/src/caesar_decrypt.c
)
target_include_directories(caesar PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/caesar_cipher/inc
)

# XOR shared library
add_library(xor SHARED
    xor_cipher/src/xor_encrypt.c
    xor_cipher/src/xor_decrypt.c
)
target_include_directories(xor PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/xor_cipher/inc
)