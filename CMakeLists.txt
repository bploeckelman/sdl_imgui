cmake_minimum_required(VERSION 3.20)
project(sdl_imgui)

set(CMAKE_CXX_STANDARD 17)

set(SDL_STATIC ON CACHE BOOL "" FORCE)
set(SDL_SHARED OFF CACHE BOOL "" FORCE)
add_subdirectory(libs/sdl)

set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
add_subdirectory(libs/sdl_image)

add_executable(sdl_imgui
        src/main.cpp
        )

target_link_libraries(sdl_imgui
        SDL2main SDL2-static
        SDL2_image
        )
