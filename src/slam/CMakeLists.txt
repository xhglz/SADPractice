list(APPEND libraries
    ${PROJECT_NAME}.ui
    ${PROJECT_NAME}.imu
    ${PROJECT_NAME}.gnss
    ${PROJECT_NAME}.basic
    ${third_party_libs}
)

list(APPEND LIBRARY_SOURCES
    core/cloud_convert.cc
    core/frontend.cc
    core/fusion.cc
    core/keyframe.cc
    core/loopclosure.cc
    core/measure_sync.cc
    core/optimization.cc
    core/ndt_inc.cc
    iekf/lio_iekf.cc
)
file(GLOB_RECURSE LIBRARY_HEADERS "core/*.h" "iekf/*.h")

add_library(${PROJECT_NAME}.slam ${LIBRARY_SOURCES} ${LIBRARY_HEADERS})
target_link_libraries(${PROJECT_NAME}.slam ${libraries})

add_executable(run_frontend test/run_frontend.cc)
target_link_libraries(run_frontend ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_dump_map test/run_dump_map.cc)
target_link_libraries(run_dump_map ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_optimization test/run_optimization.cc)
target_link_libraries(run_optimization ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_loopclosure test/run_loopclosure.cc)
target_link_libraries(run_loopclosure ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_split_map test/run_split_map.cc)
target_link_libraries(run_split_map ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_mapping test/run_mapping.cc)
target_link_libraries(run_mapping ${libraries} ${PROJECT_NAME}.slam)

add_executable(run_fusion_offline test/run_fusion_offline.cc)
target_link_libraries(run_fusion_offline ${libraries} ${PROJECT_NAME}.slam)
