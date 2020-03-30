message("Hello from the external repository!")

message("CMAKE_MODULE_PATH before append is " ${CMAKE_MODULE_PATH})
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "FromExternal")

message("CMAKE_MODULE_PATH after append is " ${CMAKE_MODULE_PATH})

message("CMAKE_INSTALL_PREFIX is " ${CMAKE_INSTALL_PREFIX})

# Set Properties->General->Configuration Type to Application(.exe)
# Creates the executable with the listed sources
# and adds sources to the Solution Explorer
add_executable (extern_binary testing.c)

# Creates a folder "executables" and adds target 
# project under it
set_property(TARGET extern_binary PROPERTY FOLDER "executables")

# Properties->General->Output Directory
set_target_properties(extern_binary PROPERTIES
                      RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

set(ExternCacheVarTest ON CACHE BOOL "Another variable to search for in CMakeCache")

include(CPack)
 
# Adds logic to INSTALL.vcproj to copy the compiled application to destination directory
install (TARGETS extern_binary
         RUNTIME DESTINATION "ExternPicklesDestination")