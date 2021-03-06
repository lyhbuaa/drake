include(GenerateExportHeader)
include(${LCM_USE_FILE})

if(NOT DISABLE_PYTHON)
  set(python_args PYTHON_SOURCES python_install_sources)
else()
  set(python_args)
endif()

if(JAVA_FOUND)
  set(java_args JAVA_SOURCES java_sources)
else()
  set(java_args)
endif()

lcm_wrap_types(
  C_EXPORT drake_lcmtypes
  C_SOURCES c_sources
  C_HEADERS c_install_headers
  CPP_HEADERS cpp_install_headers
  ${java_args}
  ${python_args}
  lcmt_acrobot_u.lcm
  lcmt_acrobot_x.lcm
  lcmt_acrobot_y.lcm
  lcmt_body_acceleration.lcm
  lcmt_body_motion_data.lcm
  lcmt_body_wrench_data.lcm
  lcmt_constrained_values.lcm
  lcmt_contact_information.lcm
  lcmt_contact_info_for_viz.lcm
  lcmt_contact_results_for_viz.lcm
  lcmt_desired_body_motion.lcm
  lcmt_desired_centroidal_momentum_dot.lcm
  lcmt_desired_dof_motions.lcm
  lcmt_drake_signal.lcm
  lcmt_driving_command_t.lcm
  lcmt_euler_floating_joint_state_t.lcm
  lcmt_foot_flag.lcm
  lcmt_force_torque.lcm
  lcmt_iiwa_command.lcm
  lcmt_iiwa_status.lcm
  lcmt_joint_pd_override.lcm
  lcmt_matlab_array.lcm
  lcmt_call_matlab.lcm
  lcmt_piecewise_polynomial.lcm
  lcmt_polynomial.lcm
  lcmt_polynomial_matrix.lcm
  lcmt_qp_controller_input.lcm
  lcmt_qp_input.lcm
  lcmt_quadrotor_input_t.lcm
  lcmt_quadrotor_output_t.lcm
  lcmt_resolved_contact.lcm
  lcmt_robot_state.lcm
  lcmt_scope_data.lcm
  lcmt_schunk_wsg_command.lcm
  lcmt_schunk_wsg_status.lcm
  lcmt_simple_car_config_t.lcm
  lcmt_simple_car_state_t.lcm
  lcmt_simulation_command.lcm
  lcmt_support_data.lcm
  lcmt_viewer_command.lcm
  lcmt_viewer_draw.lcm
  lcmt_viewer_geometry_data.lcm
  lcmt_viewer_link_data.lcm
  lcmt_viewer_load_robot.lcm
  lcmt_whole_body_data.lcm
  lcmt_zmp_com_observer_state.lcm
  lcmt_zmp_data.lcm
)

lcm_add_library(drake_lcmtypes C ${c_sources} ${c_install_headers})
generate_export_header(drake_lcmtypes)
target_include_directories(drake_lcmtypes INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)

drake_install_pkg_config_file(drake-lcmtypes
  TARGET drake_lcmtypes
  LIBS -ldrake_lcm_types)

lcm_add_library(drakeLCMTypes CPP ${cpp_install_headers})
target_include_directories(drakeLCMTypes INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)

drake_install_pkg_config_file(drake-lcmtypes-cpp)

lcm_install_headers(
  ${CMAKE_CURRENT_BINARY_DIR}/drake_lcmtypes_export.h
  ${c_install_headers}
  ${cpp_install_headers}
  DESTINATION "${DRAKE_INSTALL_INCLUDE_DIR}/lcmtypes"
)

install(TARGETS drake_lcmtypes drakeLCMTypes
  EXPORT ${PROJECT_NAME}-targets
  RUNTIME DESTINATION "${DRAKE_INSTALL_RUNTIME_DIR}"
  LIBRARY DESTINATION "${DRAKE_INSTALL_LIBRARY_DIR}"
  ARCHIVE DESTINATION "${DRAKE_INSTALL_LIBRARY_DIR}"
  INCLUDES DESTINATION "${DRAKE_INSTALL_INCLUDE_DIR}/lcmtypes"
)

if(NOT DISABLE_PYTHON)
  lcm_install_python(${python_install_sources})
endif()

if(JAVA_FOUND)
  if(NOT TARGET lcm-java)
    message(FATAL_ERROR "lcm-java not found; was LCM built with Java support?")
  endif()

  add_jar(lcmtypes_drake-java
    OUTPUT_NAME lcmtypes_drake
    INCLUDE_JARS lcm-java
    SOURCES ${java_sources}
  )

  install_jar(lcmtypes_drake-java share/java)
endif()
