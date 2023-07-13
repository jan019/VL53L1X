# v3.21 implemented semantic changes regarding $<TARGET_OBJECTS:...>
# See https://cmake.org/cmake/help/v3.21/command/target_link_libraries.html#linking-object-libraries-via-target-objects
cmake_minimum_required(VERSION 3.21)

add_library(VL53L1X INTERFACE)
add_library(VL53L1X_usage INTERFACE)

target_include_directories(VL53L1X_usage INTERFACE
  .
)


target_link_libraries(VL53L1X_usage INTERFACE
  base_config
  Wire
)

target_link_libraries(VL53L1X INTERFACE VL53L1X_usage)



add_library(VL53L1X_bin OBJECT EXCLUDE_FROM_ALL
  VL53L1X.cpp
)
target_link_libraries(VL53L1X_bin PUBLIC VL53L1X_usage)

target_link_libraries(VL53L1X INTERFACE
  VL53L1X_bin
  $<TARGET_OBJECTS:VL53L1X_bin>
)

