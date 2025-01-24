# Copyright (c) OpenMMLab. All rights reserved.
cmake_minimum_required(VERSION 3.14)

include(${CMAKE_SOURCE_DIR}/cmake/cuda.cmake NO_POLICY_SCOPE)
project(mmdeploy_cuda_device CUDA CXX)

if (${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.18.0")
    # suppress 'CMAKE_CUDA_ARCHITECTURES' warning
    cmake_policy(SET CMP0104 OLD)
endif ()

include(${CMAKE_SOURCE_DIR}/cmake/MMDeploy.cmake)

set(SRCS
        cuda_device.cpp
        cuda_builtin_kernels.cu)
mmdeploy_add_module(${PROJECT_NAME} "${SRCS}")
target_include_directories(${PROJECT_NAME} PUBLIC ${CUDA_INCLUDE_DIRS})
target_link_directories(${PROJECT_NAME} PUBLIC ${CUDA_TOOLKIT_ROOT_DIR}/lib64)
target_link_libraries(${PROJECT_NAME} PRIVATE cudart cuda)
add_library(mmdeploy::device::cuda ALIAS ${PROJECT_NAME})
