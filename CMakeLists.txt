cmake_minimum_required(VERSION 3.15)
project(CppDevOpsDemo VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(app src/main.cpp)

# Define installation target (CPack requires this)
install(TARGETS app DESTINATION bin)

# -------------------------------------------------------------
# CPack Packaging Configuration
# -------------------------------------------------------------
set(CPACK_PACKAGE_NAME "CppDevOpsDemo")
set(CPACK_PACKAGE_VENDOR "DevOps Demo")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Automated Cross-Platform C++ Application")
set(CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set(CPACK_PACKAGE_CONTACT "developer@example.com")

# Linux DEB Package specifics
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Developer")
set(CPACK_DEBIAN_PACKAGE_SECTION "utils")

# Windows MSI Package specifics
set(CPACK_WIX_UPGRADE_GUID "12345678-1234-1234-1234-123456789abc")

include(CPack)
