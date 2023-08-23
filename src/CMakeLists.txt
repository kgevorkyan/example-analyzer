set(AnalyzerSources SimplePass.cpp Sarif.cpp)

add_library(Analyzer SHARED ${AnalyzerSources})

find_package(LLVM 12.0.0 REQUIRED)

if (NOT "12.0.0" VERSION_EQUAL "${LLVM_VERSION}")
    message(FATAL_ERROR "Found LLVM ${LLVM_VERSION}, but need 12.0.0")
endif ()

target_include_directories(Analyzer PRIVATE "${CMAKE_SOURCE_DIR}/include")
target_include_directories(Analyzer PRIVATE ${LLVM_INCLUDE_DIRS})

target_link_libraries(Analyzer PRIVATE ${LLVM_LIBS})
message(STATUS "LLVM version: ${LLVM_VERSION}")
