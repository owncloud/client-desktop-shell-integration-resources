cmake_minimum_required(VERSION 3.18)

# we need at least one language for GNUInstallDirs
project(client-desktop-shell-integration-resources VERSION 1.1.0 LANGUAGES C)

include(FeatureSummary)
feature_summary(WHAT REQUIRED_PACKAGES_NOT_FOUND FATAL_ON_MISSING_REQUIRED_PACKAGES)

# debian 10 ships 5.54.0
find_package(ECM 5.54.0 REQUIRED NO_MODULE)
set_package_properties(ECM PROPERTIES TYPE REQUIRED DESCRIPTION "Extra CMake Modules." URL "https://projects.kde.org/projects/kdesupport/extra-cmake-modules")
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules ${ECM_MODULE_PATH} ${CMAKE_MODULE_PATH})


include(GNUInstallDirs)
include(ECMSetupVersion)


if( UNIX AND NOT APPLE )
    FOREACH(size 128x128 16x16 256x256 32x32 48x48 64x64 72x72)
    file(GLOB files  "${size}/*.png")
    FOREACH( file ${files} )
        file(RELATIVE_PATH outName "${CMAKE_CURRENT_SOURCE_DIR}/${size}" "${file}")
        STRING(REPLACE "oC" "ownCloud" outName ${outName})
        install(FILES ${file} DESTINATION ${CMAKE_INSTALL_DATADIR}/icons/hicolor/${size}/apps RENAME ${outName})
    ENDFOREACH(file)
    ENDFOREACH(size)

    configure_package_config_file(
            "${CMAKE_CURRENT_SOURCE_DIR}/ownCloudShellResourcesConfig.cmake.in"
            "${CMAKE_CURRENT_BINARY_DIR}/ownCloudShellResourcesConfig.cmake"
            INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/ownCloudShellResources"
    )

    ecm_setup_version(PROJECT
            VARIABLE_PREFIX OWNCLOUD_SHEEL_RESORUCES
            PACKAGE_VERSION_FILE "${CMAKE_CURRENT_BINARY_DIR}/ownCloudShellResourcesConfigVersion.cmake")
    install(FILES
            "${CMAKE_CURRENT_BINARY_DIR}/ownCloudShellResourcesConfig.cmake"
            "${CMAKE_CURRENT_BINARY_DIR}/ownCloudShellResourcesConfigVersion.cmake"
            DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/ownCloudShellResources"
            COMPONENT Devel
    )
endif()

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
