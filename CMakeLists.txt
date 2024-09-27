cmake_minimum_required(VERSION 3.28)
project(stm32_bootloader)

# Project specific settings
set(application_name "stm32_bootloader")
add_compile_definitions(STM32F446xx)

add_subdirectory(src)