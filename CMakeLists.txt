file(GLOB_RECURSE WOLFSSL_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/*.c"
)

list(REMOVE_ITEM WOLFSSL_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/aes_asm.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/aes_gcm_asm.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/fe_x25519_asm.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/sp_x86_64_asm.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/port/Espressif/esp32_mp.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/port/Espressif/esp32_aes.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/wolfcrypt/src/port/Espressif/esp32_sha.c"
)

idf_component_register(
    SRCS ${WOLFSSL_SOURCES}
    INCLUDE_DIRS "include" "."
    REQUIRES freertos esptool_py nvs_flash lwip esp_system
)

target_compile_options(${COMPONENT_LIB} PRIVATE
    -Wno-unused-function
    -Wno-unused-variable
    -Wno-deprecated-declarations
    -Wno-cpp
)

target_compile_definitions(${COMPONENT_LIB} PRIVATE
    WOLFSSL_USER_SETTINGS
)