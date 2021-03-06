set(LEELOO_INCLUDE_U8 0)
set(LEELOO_INCLUDE_U16 0)
set(LEELOO_INCLUDE_U32 0)
set(LEELOO_INCLUDE_U64 0)
foreach (INC ${LEELOO_INCLUDE})
	set(LEELOO_INCLUDE_U${INC} 1)
endforeach()

set(SRC_FILES
	bit_field.cpp
	helpers.cpp
	ip_list_intervals.cpp
	ips_parser.cpp
	list_intervals.cpp
	port.cpp
)

set(INSTANCES_EXPORTED_H ${CMAKE_CURRENT_BINARY_DIR}/include/leeloo/instances_exported.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/leeloo/instances_exported.h.in ${INSTANCES_EXPORTED_H})

set(CONFIG_H ${CMAKE_CURRENT_BINARY_DIR}/include/leeloo/config.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/leeloo/config.h.in ${CONFIG_H})

set(HEADER_DIST_FILES
	include/leeloo/atomic_helpers.h
	include/leeloo/bench.h
	include/leeloo/bit_field.h
	include/leeloo/bits_permutation.h
	include/leeloo/exports.h
	include/leeloo/helpers.h
	include/leeloo/integer_cast.h
	include/leeloo/interval.h
	include/leeloo/intrinsics.h
	include/leeloo/ip_list_intervals.h
	include/leeloo/ip_list_intervals_with_properties.h
	include/leeloo/ips_parser.h
	include/leeloo/list_intervals.h
	include/leeloo/list_intervals_properties.h
	include/leeloo/list_intervals_random.h
	include/leeloo/list_intervals_with_properties.h
	include/leeloo/math_helpers.h
	include/leeloo/port.h
	include/leeloo/port_interval.h
	include/leeloo/port_list_intervals.h
	include/leeloo/prime_helpers.h
	include/leeloo/random.h
	include/leeloo/sort_permute.h
	include/leeloo/uni.h
	include/leeloo/uprng.h
	include/leeloo/utility.h
	${INSTANCES_EXPORTED_H}
	${CONFIG_H}
)

include_directories(${Boost_INCLUDE_DIRS})
include_directories(${TBB_INCLUDE_DIR})

add_library(leeloo SHARED ${SRC_FILES})
set(LINK_LIBRARIES ${TBB_LIBRARIES} ${Boost_LIBRARIES})
target_link_libraries(leeloo ${LINK_LIBRARIES})

install(TARGETS leeloo LIBRARY DESTINATION lib)
install(FILES ${HEADER_DIST_FILES} DESTINATION include/leeloo)
