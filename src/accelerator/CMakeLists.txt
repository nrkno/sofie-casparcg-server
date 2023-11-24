cmake_minimum_required (VERSION 3.16)
project (accelerator)

set(SOURCES
	ogl/image/image_kernel.cpp
	ogl/image/image_mixer.cpp
	ogl/image/image_shader.cpp

	ogl/util/buffer.cpp
	ogl/util/device.cpp
	ogl/util/shader.cpp
	ogl/util/texture.cpp

	accelerator.cpp
)
set(HEADERS
	ogl/image/image_kernel.h
	ogl/image/image_mixer.h
	ogl/image/image_shader.h

	ogl/util/buffer.h
	ogl/util/device.h
	ogl/util/shader.h
	ogl/util/texture.h

	ogl_image_vertex.h
	ogl_image_fragment.h

	accelerator.h
	StdAfx.h
)

bin2c("ogl/image/shader.vert" "ogl_image_vertex.h" "caspar::accelerator::ogl" "vertex_shader")
bin2c("ogl/image/shader.frag" "ogl_image_fragment.h" "caspar::accelerator::ogl" "fragment_shader")

add_library(accelerator ${SOURCES} ${HEADERS})
target_compile_features(accelerator PRIVATE cxx_std_17)
target_include_directories(accelerator PRIVATE
    ..
    ${CMAKE_CURRENT_BINARY_DIR}
    ${BOOST_INCLUDE_PATH}
    ${TBB_INCLUDE_PATH}
    ${GLEW_INCLUDE_PATH}
    ${FFMPEG_INCLUDE_PATH}
    ${SFML_INCLUDE_PATH}
    )
target_precompile_headers(accelerator PRIVATE "StdAfx.h")


source_group(sources ./.*)
source_group(sources\\cpu\\image cpu/image/.*)
source_group(sources\\cpu\\util cpu/util/.*)
source_group(sources\\ogl\\image ogl/image/.*)
source_group(sources\\ogl\\util ogl/util/.*)

target_link_libraries(accelerator common core)
