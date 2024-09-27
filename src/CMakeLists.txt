set(sources
    main.c
    stm32f4/startup_stm32f446xx.s
)

# GCC optimization level: use -O0 in debug build, otherwise -O2
if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(opt_level -O0)
else()
  set(opt_level -Os)
endif()

set(hex_file ${application_name}.hex)
set(map_file ${application_name}.map)

add_executable(${hex_file} ${sources})
target_include_directories(${hex_file} PUBLIC stm32f4)
target_include_directories(${hex_file} PUBLIC ../CMSIS_6/CMSIS/Core/Include)

set(additional_compiler_flags ${opt_level} -mcpu=cortex-m4)
set(additional_linker_flags -Wl,-Map=${map_file},--cref,--no-warn-mismatch,-T${CMAKE_CURRENT_SOURCE_DIR}/stm32f4/stm32f4.ld)

target_compile_options(${hex_file} PRIVATE ${additional_compiler_flags})
target_link_libraries(${hex_file} PRIVATE ${additional_linker_flags})