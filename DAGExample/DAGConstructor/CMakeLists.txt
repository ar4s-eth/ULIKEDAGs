cmake_minimum_required ( VERSION 3.1 )

project(DAGConstructor LANGUAGES CXX CUDA)

find_package(OpenGL REQUIRED) #FIXME: Remove. Need dependencies because of CudaHelpers....
find_package(GLEW REQUIRED)	#FIXME: Remove. Need dependencies because of CudaHelpers....
#find_package(CUDA REQUIRED)
#list(APPEND CMAKE_CUDA_FLAGS " -gencode=arch=compute_52,code=sm_52")
#list( APPEND CMAKE_CUDA_FLAGS " -gencode=arch=compute_75,code=sm_75 -use_fast_math")
list( APPEND CMAKE_CUDA_FLAGS ${PROJECT_CUDA_FLAGS})


add_library(DAGConstructor STATIC
			DAGConstructor/DAGConstructor.cu
			DAGConstructor/DAGConstructor.h
			DAGConstructor/Merger.cpp
			DAGConstructor/Merger.h
)

target_link_libraries(DAGConstructor
	PRIVATE
		OpenGL::GL #FIXME: Remove. Need dependencies because of CudaHelpers....
		GLEW::GLEW #FIXME: Remove. Need dependencies because of CudaHelpers....
		glm
)
target_link_libraries(DAGConstructor
	PRIVATE 
		DAG
		utils
)

target_include_directories( DAGConstructor 
	PUBLIC
		$<BUILD_INTERFACE:${DAGConstructor_BINARY_DIR}>
		$<BUILD_INTERFACE:${DAGConstructor_SOURCE_DIR}>
		$<INSTALL_INTERFACE:include>
)

set_property ( TARGET DAGConstructor PROPERTY CXX_STANDARD_REQUIRED ON )
set_property ( TARGET DAGConstructor PROPERTY CXX_EXTENSIONS ON )
set_property ( TARGET DAGConstructor PROPERTY CXX_STANDARD 17 )
