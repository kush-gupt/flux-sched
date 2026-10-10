add_library(sched-fluxion-resource-module SHARED
    ${CMAKE_CURRENT_SOURCE_DIR}/resource_match.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/resource_match.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/resource_match_opts.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/resource_match_opts.hpp
    )
target_link_libraries (sched-fluxion-resource-module PUBLIC
    resource
    PkgConfig::JANSSON
    PkgConfig::UUID
    cppwrappers
    )
set_target_properties(sched-fluxion-resource-module PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    )
install(TARGETS sched-fluxion-resource-module LIBRARY)

flux_add_plugin ( sched-fluxion-resource MODULE
    ${CMAKE_CURRENT_SOURCE_DIR}/resource.cpp
    )
flux_add_plugin ( sched-fluxion-feasibility MODULE
    ${CMAKE_CURRENT_SOURCE_DIR}/feasibility.cpp
    )

target_link_libraries (sched-fluxion-resource PRIVATE
	sched-fluxion-resource-module
    )
target_link_libraries (sched-fluxion-feasibility PRIVATE
	sched-fluxion-resource-module
    )
