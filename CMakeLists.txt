cmake_minimum_required(VERSION 3.20)
project(sdl_imgui)

set(CMAKE_CXX_STANDARD 17)

set(SDL_STATIC ON CACHE BOOL "" FORCE)
set(SDL_SHARED OFF CACHE BOOL "" FORCE)
add_subdirectory(libs/sdl)

set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
add_subdirectory(libs/sdl_image)

# NOTE: can't just add_subdirectory(libs/imgui)
# because it doesn't contain a CMakeLists.txt file
# so it has to be added as a library instead.

# Should be able to build with just these sources:
# libs/imgui/imgui*.cpp (except imgui_demo.cpp unless we want to run the demo content)
# libs/imgui/backends/imgui_impl_sdl.cpp
# libs/imgui/backends/imgui_impl_opengl3.cpp
add_library(imgui
        libs/imgui/imgui.cpp
        libs/imgui/imgui_demo.cpp
        libs/imgui/imgui_draw.cpp
        libs/imgui/imgui_tables.cpp
        libs/imgui/imgui_widgets.cpp
        libs/imgui/backends/imgui_impl_sdl.cpp
        libs/imgui/backends/imgui_impl_opengl3.cpp
        )
# Make sure the backend source files can find required headers
target_include_directories(imgui PRIVATE
        libs/imgui
        libs/sdl/include
        )

add_executable(sdl_imgui
        src/main.cpp
        )

include_directories(sdl_imgui PRIVATE
        libs/sdl/include
        libs/sdl_image
        libs/imgui
        libs/imgui/backends
        )

target_link_libraries(sdl_imgui
        opengl32
        SDL2main SDL2-static
        SDL2_image
        imgui
        )
