project(cppipc)

if(WIN32)
  SET(PLATFORM_SOURCES client/console_cancel_handler_win.cpp)
else()
  SET(PLATFORM_SOURCES client/console_cancel_handler_unix.cpp)
endif()

# Libraries should not link both cppipc and cppipc_zookeeper together
# They are not compatible
make_library(cppipc
  SOURCES
    client/comm_client.cpp
    ${PLATFORM_SOURCES}
    common/message_types.cpp
    common/object_factory.cpp
    common/object_factory_impl.cpp
    common/ipc_deserializer.cpp
    server/comm_server.cpp
  REQUIRES
    nanosockets boost logger cancel_serverside_ops minipsutil_static
)

make_library(cancel_serverside_ops
  SOURCES
    server/cancel_ops.cpp
)
