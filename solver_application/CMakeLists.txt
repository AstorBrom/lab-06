cmake_minimum_required(VERSION 3.4)

project(solve_app)

add_executable(gg equation.cpp)

set_target_properties(${PROJECT_NAME} PROPERTIES
                        CMAKE_CXX_STANDARD 17
                        CMAKE_CXX_STANDARD_REQUIRED ON
                        CMAKE_BUILD_TYPE Release)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
                                                   ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib   
                                                   ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
                                                   ${CMAKE_CURRENT_SOURCE_DIR}/../solver_application)
						   
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib formatterr)						   
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_exx)                                                
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solverr)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_application solve_appp)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../hello_world_application helloo)

target_link_libraries(gg formatter_ex solver formatter hello solve_app)
if(make_bin)
	install(TARGETS solve_app RUNTIME DESTINATION bin)
	set(CPACK_GENERATOR "DEB")
	set(CPACK_DEBIAN_PACKAGE_MAINTAINER "David Doria")
	set(CPACK_DEBIAN_FILE_NAME "solvering.deb")
	set(CPACK_GENERATOR "DragNDrop")
	set(CPACK_PACKAGE_FILE_NAME "solvering_dmg")
	set(CPACK_GENERATOR "RPM")
	set(CPACK_RPM_FILE_NAME solvering.rpm)
	set(CPACK_GENERATOR "WIX")
	set(CPACK_PACKAGE_FILE_NAME "wixxx")
else()
	install(FILES equation.cpp DESTINATION src)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/libformatter_ex.a DESTINATION src)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib/libformatter.a DESTINATION src)
	install(TARGETS solverlib DESTINATION src)
	set(CPACK_GENERATOR "TGZ")
	set(CPACK_PACKAGE_FILE_NAME "just_code")
endif()
include(CPack)
