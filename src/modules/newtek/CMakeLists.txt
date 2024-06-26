cmake_minimum_required (VERSION 3.16)
project (newtek)

set(SOURCES
		consumer/newtek_ndi_consumer.cpp

		producer/newtek_ndi_producer.cpp

		util/ndi.cpp

		newtek.cpp

)
set(HEADERS
		consumer/newtek_ndi_consumer.h

		producer/newtek_ndi_producer.h

		util/ndi.h

		newtek.h

		interop/Processing.NDI.compat.h
		interop/Processing.NDI.deprecated.h
		interop/Processing.NDI.DynamicLoad.h
		interop/Processing.NDI.Find.h
		interop/Processing.NDI.FrameSync.h
		interop/Processing.NDI.Lib.cplusplus.h
		interop/Processing.NDI.Lib.h
		interop/Processing.NDI.Recv.ex.h
		interop/Processing.NDI.Recv.h
		interop/Processing.NDI.Routing.h
		interop/Processing.NDI.Send.h
		interop/Processing.NDI.structs.h
		interop/Processing.NDI.utilities.h

		StdAfx.h
)

if (MSVC)
	list(APPEND SOURCES util/air_send.cpp consumer/newtek_ivga_consumer.cpp)
	list(APPEND HEADERS util/air_send.h consumer/newtek_ivga_consumer.h)
endif()

add_library(newtek ${SOURCES} ${HEADERS})
target_compile_features(newtek PRIVATE cxx_std_17)
target_include_directories(newtek PRIVATE
    ..
    ../..
    ${BOOST_INCLUDE_PATH}
    ${TBB_INCLUDE_PATH}
    ${FFMPEG_INCLUDE_PATH}
    )
target_precompile_headers(newtek PRIVATE "StdAfx.h")
configure_file("${PROJECT_SOURCE_DIR}/packages.config" "${CMAKE_CURRENT_BINARY_DIR}/packages.config")

set_target_properties(newtek PROPERTIES FOLDER modules)
source_group(sources\\consumer consumer/*)
source_group(sources\\producer producer/*)
source_group(sources\\interop interop/*)
source_group(sources\\util util/*)
source_group(sources ./*)

target_link_libraries(newtek
	common
	core
    ffmpeg
)

casparcg_add_include_statement("modules/newtek/newtek.h")
casparcg_add_init_statement("newtek::init" "newtek")
casparcg_add_module_project("newtek")
