idf_component_register(
    SRCS ${WOLFSSL_SOURCES}
    INCLUDE_DIRS "include" "."
    REQUIRES freertos esptool_py nvs_flash        # ← add freertos here
)
