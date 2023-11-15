1. Cmake is a build system generator for c++ code. i.e it generates makefiles or any other platform dependent files to build the project.
2. Custom DSL to define the build process. DSL mostly looks like a list of function call invokations.
3. The DSLs and their purpose are given below
   1. project(name) - define the project with a name.
   2. cmake_minimum_required() - define the minimum cmake version.
   3. add_executable(NAME files) - create executable with the given files
   4. add_library(NAME files) - create a static i.e *.a library with the given files
   5. target_include_directories(EXECUTABLE path) - Add path to the include option while building the executable.
   6. configure_file(original_file final_file) - template expansion of the original_file to the final_file. Variables are marked as @variable@
   7. set(FLAG value) - Set the value of the flag to value
   8. target_link_libraries(EXECUTABLE lib) - Use lib while building the executable
   9. add_subdirectory(directory) - Add directory and files in it to the current build directory
   10. if - conditional execution
4. Use cmake <folder> command to generate and populate the build folder. cmake --build . to generate the build.
   
