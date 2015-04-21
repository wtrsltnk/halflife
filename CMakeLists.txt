cmake_minimum_required(VERSION 2.6)

project(run-jump-retry)

if(${CMAKE_BUILD_TYPE} MATCHES DEBUG)
    message(STATUS "CMAKE_BUILD_TYPE: Debug")
else()
    message(STATUS "CMAKE_BUILD_TYPE: Release")
endif(${CMAKE_BUILD_TYPE} MATCHES DEBUG)

add_subdirectory(dlls)
add_subdirectory(cl_dll)

if(DEFINED MOD_FOLDER)
    if(NOT DEFINED MOD_DLL_INSTALL_FOLDER)
        set(MOD_DLL_INSTALL_FOLDER "${MOD_FOLDER}\\dlls")
    endif(NOT DEFINED MOD_DLL_INSTALL_FOLDER)

    if(NOT DEFINED MOD_CDLL_INSTALL_FOLDER)
        set(MOD_CDLL_INSTALL_FOLDER "${MOD_FOLDER}\\dlls")
    endif(NOT DEFINED MOD_CDLL_INSTALL_FOLDER)

    get_target_property(HLDLL_LOCATION hldll LOCATION)
    add_custom_target(Copy_HL_DLL_To_Mod_Directory ALL
        ${CMAKE_COMMAND} -E copy ${HLDLL_LOCATION} ${MOD_DLL_INSTALL_FOLDER}
    )
    add_dependencies(Copy_HL_DLL_To_Mod_Directory ${ALL_TARGETS})

    get_target_property(HL_CDLL_LOCATION hl_cdll LOCATION)
    add_custom_target(Copy_HL_CDLL_To_Mod_Directory ALL
        ${CMAKE_COMMAND} -E copy ${HL_CDLL_LOCATION} ${MOD_CDLL_INSTALL_FOLDER}
    )
    add_dependencies(Copy_HL_CDLL_To_Mod_Directory ${ALL_TARGETS})
endif(DEFINED MOD_FOLDER)
