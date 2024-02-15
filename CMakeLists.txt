# Copyright (C) 2007-2012 LuaDist.
# Created by Peter Drahoš
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

project ( luabitop C )
cmake_minimum_required ( VERSION 2.8 )
#include ( cmake/dist.cmake )
#include ( lua )
#
#install_lua_module ( bit bit.c bit.def )
#
#add_lua_test ( bittest.lua )
#add_lua_test ( nsievebits.lua )
#add_lua_test ( md5test.lua )
#
#install_doc ( doc/ )
#install_data ( README )
#install_foo ( bitbench.lua nsievebits.lua md5test.lua )
#install_test ( bittest.lua )

set(CPM_DOWNLOAD_LOCATION "${CMAKE_BINARY_DIR}/cmake/CPM.cmake")
if(NOT (EXISTS ${CPM_DOWNLOAD_LOCATION}))
    file(DOWNLOAD https://github.com/cpm-cmake/CPM.cmake/releases/download/v0.38.3/CPM.cmake ${CPM_DOWNLOAD_LOCATION}
        EXPECTED_HASH SHA256=cc155ce02e7945e7b8967ddfaff0b050e958a723ef7aad3766d368940cb15494)
endif()
include(${CPM_DOWNLOAD_LOCATION})

CPMAddPackage(
    NAME lua51
    GITHUB_REPOSITORY GameDevDeps/lua51
    GIT_TAG lua/5.1.5)

find_package(lua51 REQUIRED)

add_library(luabitop.luabitop-static STATIC ${CMAKE_CURRENT_SOURCE_DIR}/bit.c)
add_library(luabitop::luabitop-static ALIAS luabitop.luabitop-static)
target_link_libraries(luabitop.luabitop-static PUBLIC lua51.liblua-static)
set_target_properties(luabitop.luabitop-static PROPERTIES EXPORT_NAME luabitop-static OUTPUT_NAME luabitop-static)
