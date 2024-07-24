cmake_minimum_required(VERSION 3.18)

project(client-desktop-shell-integration-resources VERSION 1.0.0)

include(FeatureSummary)
feature_summary(WHAT REQUIRED_PACKAGES_NOT_FOUND FATAL_ON_MISSING_REQUIRED_PACKAGES)

find_package(ECM 6.0.0 REQUIRED NO_MODULE)
set_package_properties(ECM PROPERTIES TYPE REQUIRED DESCRIPTION "Extra CMake Modules." URL "https://projects.kde.org/projects/kdesupport/extra-cmake-modules")
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules ${ECM_MODULE_PATH} ${CMAKE_MODULE_PATH})


include(KDEInstallDirs)


if( UNIX AND NOT APPLE )
    FOREACH(size 128x128 16x16 256x256 32x32 48x48 64x64 72x72)
    file(GLOB files  "${size}/*.png")
    FOREACH( file ${files} )
        file(RELATIVE_PATH outName "${CMAKE_CURRENT_SOURCE_DIR}/${size}" "${file}")
        STRING(REPLACE "oC" "ownCloud" outName ${outName})
        install(FILES ${file} DESTINATION ${KDE_INSTALL_DATADIR}/icons/hicolor/${size}/apps RENAME ${outName})
    ENDFOREACH(file)
    ENDFOREACH(size)
endif()

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
