message("Hello from the external repository!")

# Set Properties->General->Configuration Type to Application(.exe)
# Creates app.exe with the listed sources (main.cxx)
# Adds sources to the Solution Explorer
add_executable (extern_binary testing.c)

# Properties->Linker->Input->Additional Dependencies
target_link_libraries (extern_binary  math)

# Creates a folder "executables" and adds target 
# project (app.vcproj) under it
set_property(TARGET extern_binary PROPERTY FOLDER "executables")

# Properties->General->Output Directory
set_target_properties(extern_binary PROPERTIES
                      RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

# Adds logic to INSTALL.vcproj to copy app.exe to destination directory
install (TARGETS extern_binary
         RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/_install)