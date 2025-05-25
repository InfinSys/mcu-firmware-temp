
#=======================================
#     /tests/host Directory Script
#=======================================



if(UNIT_TESTING)
	add_subdirectory(unit)
endif()

if(BENCHMARKING)
	add_subdirectory(benchmark)
endif()
