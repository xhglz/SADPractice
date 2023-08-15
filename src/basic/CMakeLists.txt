
add_subdirectory(msg)

# library ui -------------------------------
add_library(${PROJECT_NAME}.ui
    ui/ui_car.cc
    ui/ui_cloud.cc
    ui/ui_trajectory.cc
    ui/pangolin_window.cc
    ui/pangolin_window_impl.cc
)
target_link_libraries(${PROJECT_NAME}.ui
    ${third_party_libs}
)

# library imu --------------------------------
add_library(${PROJECT_NAME}.imu
    imu/static_imu_init.cc
    imu/imu_preintegration.cc
)
target_link_libraries(${PROJECT_NAME}.imu
    ${third_party_libs}
)

# library gnss -------------------------------
add_library(${PROJECT_NAME}.gnss
    gnss/utm.cc
    gnss/tranmerc.cc
    gnss/utm_convert.cc
)
target_link_libraries(${PROJECT_NAME}.gnss
    ${third_party_libs}
)

# library basic -------------------------------
add_library(${PROJECT_NAME}.basic
    io/io_utils.cc
    timer/timer.cc
    types/g2o_types.cc
    utils/global_flags.cc
    pointcloud/packets_parser.cc
    pointcloud/point_cloud_utils.cc
    pointcloud/velodyne_convertor.cc
)
target_link_libraries(${PROJECT_NAME}.basic
    ${PROJECT_NAME}.ui
    ${catkin_LIBRARIES}
    ${PCL_LIBRARIES}
)

# ROS sensor message ------------------------
set(sad_messages
    monitor_msgs_generate_messages
    velodyne_msgs_generate_messages
    livox_ros_driver_generate_messages
)
add_dependencies(${PROJECT_NAME}.basic ${sad_messages})

# test -------------------------------
add_executable(ui_test test/ui_test.cc)
target_link_libraries(ui_test
    ${PROJECT_NAME}.ui
    ${third_party_libs}
)