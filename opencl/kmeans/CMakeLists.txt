#https://streamcomputing.eu/blog/2015-09-25/handling-opencl-with-cmake-3-1-and-higher/
#Minimal OpenCL CMakeLists.txt by StreamComputing
cmake_minimum_required (VERSION 3.1)
project(kmeans)

if(ARM_LINUX_SYSROOT)
	# --------------------------------------------------
	# switch searching path to arm linux
	# --------------------------------------------------
	message("ARM_LINUX_SYSROOT=${ARM_LINUX_SYSROOT}")
	set( CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER )
	set( CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY )
	set( CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY )
	set(OPENCL_VER "${OPENCL_VER}")
	set(OpenCL_INCLUDE_DIRS "${OPENCL_INC}")
	set(OpenCL_LIBRARY "${OPENCL_LIB}/libOpenCL.so")
	message("OpenCL_LIBRARY=${OpenCL_LIBRARY}")
	include_directories(${OpenCL_INCLUDE_DIRS})
	message("OpenCL_INCLUDE_DIRS=${OpenCL_INCLUDE_DIRS}")
elseif(ANDROID_NDK)
else()
	# Handle OpenCL
	find_package(OpenCL REQUIRED)
	message("OpenCL_FOUND : ${OpenCL_FOUND}")
	if(OpenCL_FOUND)
		message("OpenCL_INCLUDE_DIRS=${OpenCL_INCLUDE_DIRS}")
		message("OpenCL_LIBRARY=${OpenCL_LIBRARY}")
		include_directories(${OpenCL_INCLUDE_DIRS})
	endif()
endif()

# --------------------------------------------------
# Organize output files.  On Windows this also keeps .dll files next
# to the .exe files that need them, making tests easy to run.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${kmeans_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${kmeans_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${kmeans_BINARY_DIR}/lib)
message("kmeans_BINARY_DIR ${kmeans_BINARY_DIR}")
message("CMAKE_LIBRARY_OUTPUT_DIRECTORY =${CMAKE_LIBRARY_OUTPUT_DIRECTORY}")

#link_directories(${OpenCL_LIBRARY})
add_executable (kmeans
	kmeans.cpp
	cluster.c
	getopt.c
	read_input.c
	kmeans_clustering.c
	rmse.c
	)

target_link_libraries (kmeans
	${OpenCL_LIBRARY}
	)
