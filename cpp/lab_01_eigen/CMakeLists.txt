cmake_minimum_required( VERSION 3.5.1 )

project(lab_01_eigen)
set(exe_name lab_01_eigen)

# Find libraries
find_package(Eigen3 REQUIRED)

add_executable(${exe_name}
  main.cpp
  )

target_link_libraries(${exe_name}
  Eigen3::Eigen
  )

set_target_properties(${exe_name} PROPERTIES
  CXX_STANDARD_REQUIRED ON
  CXX_STANDARD 17
  )

set(gcc_like_cxx "$<COMPILE_LANG_AND_ID:CXX,ARMClang,AppleClang,Clang,GNU,LCC>")
set(msvc_cxx "$<COMPILE_LANG_AND_ID:CXX,MSVC>")

target_compile_options(${exe_name} PRIVATE
  "$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wpedantic;-Wshadow;-Wformat=2>>"
  "$<${msvc_cxx}:$<BUILD_INTERFACE:-W4>>"
  )

target_compile_definitions(${exe_name} PUBLIC
  "$<${msvc_cxx}:-D_USE_MATH_DEFINES>"
  )
