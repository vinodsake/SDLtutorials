cmake_minimum_required(VERSION 3.10)

project(SDLTUTORIALS)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
find_package(SDL2 REQUIRED)
### Having issues with find_packages for SDL2_image, SDL2_mixer & SDL2_ttf. 
### Provided hack to include all required headers and libraries 
#find_package(SDL2_image REQUIRED)
#find_package(SDL2_ttf REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS} ${SDL2_IMAGE_INCLUDE_DIRS} ${SDL2_TTF_INCLUDE_DIRS})

file(GLOB SUBDIR RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/*)
foreach(SUBDIRS ${SUBDIR})
	if(IS_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/${SUBDIRS})
		if(${SUBDIRS} STREQUAL "_build" OR ${SUBDIRS} STREQUAL ".git")
		else()
			add_subdirectory(${SUBDIRS})
		endif()	
	endif()
endforeach()
