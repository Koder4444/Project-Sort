cmake_minimum_required (VERSION 3.18)

# Enable Hot Reload for MSVC
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project("Project-Sort" LANGUAGES CXX)

add_executable(ProjectSort "src/Project-Sort.cpp")

target_compile_features(ProjectSort PUBLIC cxx_std_17)

if(MSVC)
    target_link_options(ProjectSort PRIVATE "/STACK:32000000")
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    target_link_options(ProjectSort PRIVATE "-Wl,--stack,32000000")
endif()
