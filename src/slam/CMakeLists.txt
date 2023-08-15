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

# add_executable(run_optimization run_optimization.cc)
# target_link_libraries(run_optimization
#         ${PROJECT_NAME}.ch9
#         ${third_party_libs}
#         )

# add_executable(run_loopclosure run_loopclosure.cc)
# target_link_libraries(run_loopclosure
#         ${PROJECT_NAME}.ch9
#         ${third_party_libs}
#         )

# add_executable(run_mapping run_mapping.cc)
# target_link_libraries(run_mapping
#         ${PROJECT_NAME}.ch9
#         ${third_party_libs}
#         )

# add_executable(dump_map dump_map.cc)
# target_link_libraries(dump_map
#         ${PROJECT_NAME}.ch9
#         ${PROJECT_NAME}.common
#         ${third_party_libs}
#         )

# add_executable(split_map split_map.cc)
# target_link_libraries(split_map
#         ${PROJECT_NAME}.ch9
#         ${PROJECT_NAME}.common
#         ${third_party_libs}
#         )
