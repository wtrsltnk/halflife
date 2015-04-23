cmake_minimum_required(VERSION 2.8)

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

	message(STATUS "Will copy rjr_server to ${MOD_DLL_INSTALL_FOLDER}")
	add_custom_target(Copy_HL_DLL_To_Mod_Directory ALL
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\dlls\\rjr_server.dll" ${MOD_DLL_INSTALL_FOLDER}
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\dlls\\rjr_server.pdb" ${MOD_DLL_INSTALL_FOLDER}
    )
    add_dependencies(Copy_HL_DLL_To_Mod_Directory ${ALL_TARGETS})

	message(STATUS "Will copy rjr_client to ${MOD_CDLL_INSTALL_FOLDER}")
	add_custom_target(Copy_HL_CDLL_To_Mod_Directory ALL
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\cl_dll\\rjr_client.dll" ${MOD_CDLL_INSTALL_FOLDER}
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\cl_dll\\rjr_client.pdb" ${MOD_CDLL_INSTALL_FOLDER}
    )
    add_dependencies(Copy_HL_CDLL_To_Mod_Directory ${ALL_TARGETS})
endif(DEFINED MOD_FOLDER)
