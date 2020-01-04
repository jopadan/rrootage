#################################################################################
##
## rrootage game
## Copyright (c) 
##
## This software is provided 'as-is', without any express or implied
## warranty. In no event will the authors be held liable for any damages
## arising from the use of this software.
##
## Permission is granted to anyone to use this software for any purpose,
## including commercial applications, and to alter it and redistribute it
## freely, subject to the following restrictions:
##
## 1. The origin of this software must not be misrepresented; you must not
##    claim that you wrote the original software. If you use this software
##    in a product, an acknowledgment in the product documentation would be
##    appreciated but is not required.
##
## 2. Altered source versions must be plainly marked as such, and must not be
##    misrepresented as being the original software.
##
## 3. This notice may not be removed or altered from any source distribution.
##
#################################################################################

# Directory rrootage


cmake_minimum_required(VERSION 3.1)

project(rrootage)

set(EXECUTABLE_NAME "rr")

set(rr_SOURCES
	src/rr.c 
	src/foe.cc
	src/foecommand.cc
	src/barragemanager.cc
	src/boss.cc
	src/ship.c
	src/laser.c
	src/frag.c
	src/background.c
	src/letterrender.c 
	src/shot.c
	src/screen.c 
	src/vector.c 
	src/degutil.c 
	src/rand.c
	src/mt19937int.c
	src/soundmanager.c 
	src/attractmanager.c
)

add_executable(${EXECUTABLE_NAME} ${rr_SOURCES})


list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/sdl2)
find_package(SDL2 REQUIRED )
find_package(SDL2_mixer REQUIRED)

set (OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)
find_package(bulletml REQUIRED)

target_link_libraries(${EXECUTABLE_NAME} SDL2::Main)

if(SDL2_FOUND)
	include_directories(${SDL2_INCLUDE_DIR})
	target_link_libraries(${EXECUTABLE_NAME} ${SDL2_LIBRARIES})
endif()
if(SDL2_mixer_FOUND)
	include_directories(${SDL2_MIXER_INCLUDE_DIR})
	target_link_libraries(${EXECUTABLE_NAME} ${SDL2_MIXER_LIBRARIES})
endif()

if(OpenGL_FOUND)
	include_directories(${OPENGL_INCLUDE_DIR})
	target_link_libraries(${EXECUTABLE_NAME} ${OPENGL_LIBRARIES})
endif()

if(bulletml_FOUND)
	include_directories(${BULLETML_INCLUDE_DIR})
	target_link_libraries(${EXECUTABLE_NAME} ${BULLETML_LIBRARIES})
endif()

# Install target
install(TARGETS ${EXECUTABLE_NAME} DESTINATION bin)
install(DIRECTORY sounds/ DESTINATION share/games/rrootage)
install(DIRECTORY images/ DESTINATION share/games/rrootage)
install(DIRECTORY morph_heavy/ DESTINATION share/games/rrootage)
install(DIRECTORY morph/ DESTINATION share/games/rrootage)
install(DIRECTORY normal/ DESTINATION share/games/rrootage)
install(DIRECTORY psy/ DESTINATION share/games/rrootage)
install(DIRECTORY reversible/ DESTINATION share/games/rrootage)
install(DIRECTORY simple/ DESTINATION share/games/rrootage)
