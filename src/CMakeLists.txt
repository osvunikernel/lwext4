
option(LWEXT4_BUILD_SHARED_LIB "Build shared library" OFF)

#LIBRARY
include_directories(.)
set(LWEXT4_SRC "ext4_extent.c"
               "ext4_fs.c"
               "ext4_dir_idx.c"
               "ext4_bcache.c"
               "ext4_dir.c"
               "ext4_blockdev.c"
               "ext4_inode.c"
               "ext4_balloc.c"
               "ext4_hash.c"
               "ext4_ialloc.c"
               "ext4_super.c"
               "ext4_crc32.c"
               "ext4_bitmap.c"
               "ext4_block_group.c"
               "ext4_trans.c"
               "ext4_debug.c")
if(LWEXT4_BUILD_SHARED_LIB)
  add_library(lwext4 SHARED ${LWEXT4_SRC})
else()
  add_library(lwext4 STATIC ${LWEXT4_SRC})
endif()

if  (DEFINED SIZE)
    add_custom_target(lib_size ALL DEPENDS lwext4 COMMAND ${SIZE} liblwext4.a)
else()

endif()

if  (DEFINED INSTALL_LIB)
INSTALL(TARGETS lwext4 DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)
INSTALL(DIRECTORY ${PROJECT_BINARY_DIR}/include/. DESTINATION ${CMAKE_INSTALL_PREFIX}/include/lwext4)
endif()
