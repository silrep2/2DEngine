cmake_minimum_required(VERSION 3.0)

project(2DEngine)

MACRO(source_group_by_dir source_files source_root_dir)
	if(MSVC)
		foreach(sgbd_file ${${source_files}})
			get_filename_component(full_path ${sgbd_file} DIRECTORY )
			IF( NOT  ${${source_root_dir}} STREQUAL ${full_path}  )
				string(REGEX REPLACE ${${source_root_dir}}/ "" short_path ${full_path})
				string(REGEX REPLACE "/" "\\\\\\\\" sgbd_group_name ${short_path})
				source_group(${sgbd_group_name} FILES ${sgbd_file})
			ENDIF()
		endforeach(sgbd_file)
	endif(MSVC)
ENDMACRO(source_group_by_dir)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
file(GLOB_RECURSE PROJ_SOURCES
	${CMAKE_CURRENT_LIST_DIR}/src/*.hpp 
	${CMAKE_CURRENT_LIST_DIR}/src/*.cpp
)
source_group_by_dir( PROJ_SOURCES  CMAKE_CURRENT_LIST_DIR )
add_executable(main ${PROJ_SOURCES})