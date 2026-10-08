cmake_minimum_required(VERSION 3.15)

project(
    CppDevOpsDemo
    VERSION 1.0.0
    LANGUAGES CXX
)

# =============================================================
# C++ CONFIGURATION
# =============================================================

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# =============================================================
# APPLICATION
# =============================================================

add_executable(app
    src/main.cpp
)

# =============================================================
# INSTALLATION
# =============================================================

include(GNUInstallDirs)

install(
    TARGETS app
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# =============================================================
# CPACK GENERAL
# =============================================================

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

# =============================================================
# DEBIAN PACKAGE
# =============================================================

set(CPACK_DEBIAN_PACKAGE_NAME "cppdevopsdemo")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Developer")
set(CPACK_DEBIAN_PACKAGE_SECTION "utils")
set(CPACK_DEBIAN_PACKAGE_PRIORITY "optional")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION
    "Automated Cross-Platform C++ Application"
)

if(CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64|AMD64")
    set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "amd64")
elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "aarch64|arm64|ARM64")
    set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "arm64")
else()
    set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "${CMAKE_SYSTEM_PROCESSOR}")
endif()

# =============================================================
# RPM PACKAGE
# =============================================================

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
else()
    set(CPACK_RPM_PACKAGE_ARCHITECTURE "${CMAKE_SYSTEM_PROCESSOR}")
endif()

# =============================================================
# WINDOWS MSI / WIX 3
# =============================================================

set(CPACK_WIX_VERSION "3")

# Keep this GUID permanently associated with this product.
set(
    CPACK_WIX_UPGRADE_GUID
    "7D5E6F3A-2D94-4F7B-8C4A-9E8D7B6A5C21"
)

set(CPACK_START_MENU_SHORTCUTS CppDevOpsDemo)
set(CPACK_DESKTOP_SHORTCUTS CppDevOpsDemo)

# =============================================================
# CPACK
# =============================================================

# AppImage is generated separately with linuxdeploy.
# DEB/RPM are selected explicitly by the GitHub Actions workflow.
set(CPACK_GENERATOR "DEB;RPM")

include(CPack)
