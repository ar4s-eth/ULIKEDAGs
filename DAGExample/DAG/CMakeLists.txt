cmake_minimum_required ( VERSION 3.1 )

project(DAG)

add_library(DAG STATIC
			DAG.h
			DAG.cpp
)

target_link_libraries(DAG 
	PRIVATE 
		utils
)

target_include_directories( DAG 
	PUBLIC
		$<BUILD_INTERFACE:${DAG_BINARY_DIR}>
		$<BUILD_INTERFACE:${DAG_SOURCE_DIR}>
		$<INSTALL_INTERFACE:include>
)

target_compile_features(DAG PUBLIC cxx_std_17)

#set_property(TARGET DAG PROPERTY CXX_STANDARD_REQUIRED ON)
#set_property(TARGET DAG PROPERTY CXX_EXTENSIONS ON)
#set_property(TARGET DAG PROPERTY CXX_STANDARD 17)
