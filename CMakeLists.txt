cmake_minimum_required(VERSION 3.10)
project(ndppd C)
set(CMAKE_C_STANDARD 99)

set(CPACK_PACKAGE_VERSION_MAJOR 1)
set(CPACK_PACKAGE_VERSION_MINOR 0)
set(CPACK_PACKAGE_VERSION_PATCH 0)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/src SRC)

add_executable(ndppd ${SRC})
target_compile_options(ndppd PRIVATE -Werror -Wall -Wextra -Wno-missing-braces -Wno-missing-field-initializers)

install(
    TARGETS ndppd
    RUNTIME DESTINATION sbin
)

install(
    FILES ndppd.service
    DESTINATION "/lib/systemd/system/"
    PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ
)

set(CPACK_GENERATOR "DEB")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Toshifumi NISHINAGA")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6, init-system-helpers")
include(CPack)