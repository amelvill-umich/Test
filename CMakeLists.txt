message("Hello from the external repository!")

message("CMAKE_MODULE_PATH before append is " ${CMAKE_MODULE_PATH})
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "FromExternal")

message("CMAKE_MODULE_PATH after append is " ${CMAKE_MODULE_PATH})

message("CMAKE_INSTALL_PREFIX is " ${CMAKE_INSTALL_PREFIX})

# Set Properties->General->Configuration Type to Application(.exe)
# Creates app.exe with the listed sources (main.cxx)
# Adds sources to the Solution Explorer
add_executable (extern_binary testing.c)

# Creates a folder "executables" and adds target 
# project (app.vcproj) under it
set_property(TARGET extern_binary PROPERTY FOLDER "executables")

# Properties->General->Output Directory
set_target_properties(extern_binary PROPERTIES
                      RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

set(ExternCacheVarTest ON CACHE BOOL "Another variable to search for in CMakeCache")

# Let's see if we got the parameter passed from ExternalProject_Add, and what it was

# gives BRACKET_BINARY_DIR=C:/_FILES/home/CMake-VisualStudio-Example/build/extern-prefix/src/extern-build
# it's weird, why would the parent project give this directory? It can't have come from anywhere else...
message("BRACKET_BINARY_DIR=" ${BRACKET_BINARY_DIR})

#nothing, because the parent project didn't have ${BINARY_DIR} set to anything at all
message("VAR_BINARY_DIR=" ${VAR_BINARY_DIR})

# works, as you'd expect
message("SOMETHING_ELSE=" ${SOMETHING_ELSE}) #works

include(CPack)
 
# Adds logic to INSTALL.vcproj to copy app.exe to destination directory
install (TARGETS extern_binary
         RUNTIME DESTINATION "ExternPicklesDestination")