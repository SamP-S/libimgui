cmake_minimum_required(VERSION 3.9)

project(libimgui    VERSION 1.0.0 
                    DESCRIPTION "set of single file C/C++ libraries"
                    LANGUAGES C CXX)

# selects new opengl
if (POLICY CMP0072)
  cmake_policy (SET CMP0072 NEW)
endif(POLICY CMP0072)

set(CMAKE_CXX_STANDARD          17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

set(IMGUI_RENDERER "opengl3")
set(IMGUI_PLATFORM "sdl2")

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

find_package(OpenGL REQUIRED)
target_link_libraries(imgui PUBLIC ${OPENGL_LIBRARIES})
message(STATUS "OpenGL included at ${OPENGL_INCLUDE_DIRS}")
message(STATUS "OpenGL libraries are ${OPENGL_LIBRARIES}")

find_package(SDL2 REQUIRED)
target_include_directories(imgui PUBLIC ${SDL2_INCLUDE_DIRS})
target_link_libraries(imgui PUBLIC ${SDL2_LIBRARIES})
message(STATUS "SDL2 included at ${SDL2_INCLUDE_DIRS}")
message(STATUS "SDL2 libraries are ${SDL2_LIBRARIES}")

find_package(GLEW REQUIRED)
target_include_directories(imgui PUBLIC ${GLEW_INCLUDE_DIRS})
target_link_libraries(imgui PUBLIC ${GLEW_LIBRARIES})
message(STATUS "GLEW included at ${GLEW_INCLUDE_DIRS}")
message(STATUS "GLEW libraries are ${GLEW_LIBRARIES}")
