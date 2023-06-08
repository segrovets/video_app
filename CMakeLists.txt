cmake_minimum_required(VERSION 3.26)
project(video-app C CXX)
set(CMAKE_CXX_STANDARD 14)

add_subdirectory(lib/glfw)

if(APPLE)
    list(APPEND EXTRA_LIBS
        "-framework OpenGL"
        )
elseif(WIN32)
    list(APPEND EXTRA_LIBS
        "-lglu32 -lopenl32"
    )
    set(CMAKE_EXELINKER_FLAGS "-std=gnu99 -static -static-libgcc -static-libstdc++ -mwindows")
else()
    list(APPEND EXTRA_LIBS
        "-lGL -lGLU -lX11"
    )
endif()

add_executable(video-app src/main.cpp)
target_link_libraries(video-app glfw ${EXTRA_LIBS})
