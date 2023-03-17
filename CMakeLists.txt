cmake_minimum_required(VERSION 3.9)

project(libimgui    VERSION 1.0.0 
                    DESCRIPTION "set of single file C/C++ libraries"
                    LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD          17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

message("set imgui renderer (IMGUI_RENDERER):\n opengl3 (default),\n opengl2,\n metal,\n vulkan,\n dx9-12")
set(IMGUI_RENDERER "opengl3" CACHE STRING "")
message("set imgui platform (IMGUI_PLATFORM):\n sdl2 (default),\n glfw,\n glut,\n win32,\n osx")
set(IMGUI_PLATFORM "sdl2" CACHE STRING "set imgui platform (IMGUI_RENDERER):\n sdl2 (default),\n")

message("Platform: ${IMGUI_PLATFORM}")
message("Renderer: ${IMGUI_RENDERER}")

add_library(imgui STATIC 
    "./imgui_demo.cpp"
    "./imgui_draw.cpp"
    "./imgui_tables.cpp"
    "./imgui_widgets.cpp"
    "./imgui.cpp"
    "./backends/imgui_impl_${IMGUI_PLATFORM}.cpp"
    "./backends/imgui_impl_${IMGUI_RENDERER}.cpp"
)
target_include_directories(imgui PUBLIC "./")