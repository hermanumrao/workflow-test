cmake_minimum_required(VERSION 3.15)

project(
    CppDevOpsDemo
    VERSION 1.0.0
    LANGUAGES CXX
)

# -------------------------------------------------------------
# C++ configuration
# -------------------------------------------------------------

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# -------------------------------------------------------------
# Application
# -------------------------------------------------------------

add_executable(app
    src/main.cpp
)

# -------------------------------------------------------------
# Installation
# -------------------------------------------------------------
# This is required by CPack.
#
# Linux:
#   /usr/bin/app
#
# Windows:
#   Program Files/CppDevOpsDemo/bin/app.exe
# -------------------------------------------------------------

include(GNUInstallDirs)

install(
    TARGETS app
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# -------------------------------------------------------------
# CPack configuration
# -------------------------------------------------------------

set(CPACK_PACKAGE_NAME "CppDevOpsDemo")
set(CPACK_PACKAGE_VENDOR "DevOps Demo")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY
    "Automated Cross-Platform C++ Application"
)
set(CPACK_PACKAGE_DESCRIPTION
    "CppDevOpsDemo cross-platform C++ application."
)

set(CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set(CPACK_PACKAGE_CONTACT "developer@example.com")

# -------------------------------------------------------------
# Debian package
# -------------------------------------------------------------

set(CPACK_DEBIAN_PACKAGE_NAME "cppdevopsdemo")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Developer")
set(CPACK_DEBIAN_PACKAGE_SECTION "utils")
set(CPACK_DEBIAN_PACKAGE_PRIORITY "optional")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION
    "Automated Cross-Platform C++ Application"
)

# Automatically use the correct architecture:
#
# x86_64 -> amd64
# ARM64  -> arm64
#
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE
    "${CMAKE_SYSTEM_PROCESSOR}"
)

# Fix architecture names where required.
if(CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64|AMD64")
    set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "amd64")
elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "aarch64|arm64|ARM64")
    set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "arm64")
endif()

# -------------------------------------------------------------
# RPM package
# -------------------------------------------------------------

set(CPACK_RPM_PACKAGE_NAME "cppdevopsdemo")
set(CPACK_RPM_PACKAGE_RELEASE "1")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "Applications/Utilities")
set(CPACK_RPM_PACKAGE_DESCRIPTION
    "Automated Cross-Platform C++ Application"
)

if(CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64|AMD64")
    set(CPACK_RPM_PACKAGE_ARCHITECTURE "x86_64")
elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "aarch64|arm64|ARM64")
    set(CPACK_RPM_PACKAGE_ARCHITECTURE "aarch64")
endif()

# -------------------------------------------------------------
# Windows MSI / WiX
# -------------------------------------------------------------

set(CPACK_WIX_UPGRADE_GUID
    "7D5E6F3A-2D94-4F7B-8C4A-9E8D7B6A5C21"
)

set(CPACK_WIX_PRODUCT_GUID
    "B1F5A8C4-6D2E-4A93-9F71-3C8E5D2A7B46"
)

set(CPACK_WIX_PRODUCT_ICON
    ""
)

set(CPACK_START_MENU_SHORTCUTS
    CppDevOpsDemo
)

set(CPACK_DESKTOP_SHORTCUTS
    CppDevOpsDemo
)

# -------------------------------------------------------------
# CPack generators
# -------------------------------------------------------------
#
# The GitHub Actions workflow explicitly selects the generator:
#
#   cpack -G DEB
#   cpack -G RPM
#   cpack -G WIX
#
# Therefore we don't put AppImage here.
#
set(CPACK_GENERATOR "DEB;RPM")

include(CPack)
