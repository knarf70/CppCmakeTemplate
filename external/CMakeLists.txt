# LinAlg
set(LIBRARY_INCLUDES "linalg/")
add_library(${LIBRARY_LINALG} INTERFACE)
target_include_directories(${LIBRARY_LINALG} INTERFACE ${LIBRARY_INCLUDES})

# Loguru
# set(LOGURU_SOURCES "loguru.cpp")
file(GLOB LOGURU_SOURCES "loguru/*.cpp")
# add_library(${LIBRARY_LOG} STATIC ${LOGURU_SOURCES})
add_library(${LIBRARY_LOG} ${LOGURU_SOURCES})
target_include_directories(${LIBRARY_LOG} PUBLIC loguru) # use folder name
if(UNIX)
    target_link_libraries(${LIBRARY_LOG} PUBLIC pthread dl)
endif()

# Celero
if(USE_BENCHMARKS)
    add_subdirectory(Celero)
    add_library(${LIBRARY_BENCH} ALIAS celero)  # in celeros's own CMake, lower case is used
endif()