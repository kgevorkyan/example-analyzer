set(AnalyzerSources SimplePass.cpp Sarif.cpp)

add_library(Analyzer SHARED ${AnalyzerSources})

find_package(LLVM 14 REQUIRED)

if (NOT "14" VERSION_EQUAL "${LLVM_VERSION_MAJOR}")
    message(FATAL_ERROR "Found LLVM ${LLVM_VERSION}, but need 14")
endif ()

target_include_directories(Analyzer PRIVATE "${CMAKE_SOURCE_DIR}/include")
target_include_directories(Analyzer PRIVATE ${LLVM_INCLUDE_DIRS})

target_link_libraries(Analyzer PRIVATE ${LLVM_LIBS})
message(STATUS "LLVM version: ${LLVM_VERSION}")
