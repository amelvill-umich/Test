message("Hello from the external repository!")

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
message("BRACKET_BINARY_DIRR="${BRACKET_BINARY_DIR})
message("VAR_BINARY_DIR="${VAR_BINARY_DIR})
message("SOMETHING_ELSE="${SOMETHING_ELSE})

# Adds logic to INSTALL.vcproj to copy app.exe to destination directory
install (TARGETS extern_binary
         RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/_install)