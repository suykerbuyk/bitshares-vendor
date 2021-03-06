if ( ${CMAKE_SYSTEM_NAME} MATCHES "FreeBSD" )
    set( FREEBSD true )
    set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DOS_FREEBSD" )
    set( ENV{DBROOTDIR} /usr/local/include/db6 )
    FIND_PACKAGE( BerkeleyDB )
    #    include_directories(/usr/local/include/db46)
endif()


set( CMAKE_CXX_SOURCE_FILE_EXTENSIONS .cpp .cc )
if(APPLE)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -stdlib=libc++" )
endif(APPLE)

set( sources 
    db/builder.cc
    db/c.cc
#    db/db_bench.cc
    db/db_impl.cc
    db/db_iter.cc
    db/dbformat.cc
    db/filename.cc
#    db/leveldb_main.cc
    db/log_reader.cc
    db/log_writer.cc
    db/memtable.cc
    db/repair.cc
    db/table_cache.cc
    db/version_edit.cc
    db/version_set.cc
    db/write_batch.cc

    port/port_posix.cc

    helpers/memenv/memenv.cc

    util/arena.cc
    util/bloom.cc
    util/cache.cc
    util/coding.cc
    util/comparator.cc
    util/crc32c.cc
    util/env.cc
    util/env_posix.cc
    util/filter_policy.cc
    util/hash.cc
    util/histogram.cc
    util/logging.cc
    util/options.cc
    util/status.cc

    table/block.cc
    table/block_builder.cc
    table/filter_block.cc
    table/format.cc
    table/iterator.cc
    table/merger.cc
    table/table.cc
    table/table_builder.cc
    table/two_level_iterator.cc
)

add_library( leveldb  ${sources} )

target_include_directories(leveldb PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}"
  "${CMAKE_CURRENT_SOURCE_DIR}/include" )
target_link_libraries( leveldb pthread )
