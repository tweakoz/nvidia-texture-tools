PROJECT(nvcore)

SET(CORE_HDRS
    nvcore.h
    Array.h
    DefsGnucDarwin.h
    DefsGnucLinux.h
    DefsGnucWin32.h
    DefsVcWin32.h
    Ptr.h
    RefCounted.h
    Stream.h
    StdStream.h
    Memory.h 
    Debug.h 
    FileSystem.h 
    ForEach.h
    StrLib.h 
    TextWriter.h 
    Timer.h 
    Utils.h)

SET(CORE_SRCS ${CORE_HDRS}
    Debug.cpp
    FileSystem.cpp
    Memory.cpp
    StrLib.cpp
    TextWriter.cpp
    Timer.cpp
    )

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

# targets
ADD_DEFINITIONS(-DNVCORE_EXPORTS)

IF(UNIX)
    SET(LIBS ${LIBS} ${CMAKE_DL_LIBS})
ENDIF(UNIX)

IF(NVCORE_SHARED)
    ADD_DEFINITIONS(-DNVCORE_SHARED=1)
    ADD_LIBRARY(nvcore SHARED ${CORE_SRCS})
ELSE(NVCORE_SHARED)
    ADD_LIBRARY(nvcore ${CORE_SRCS})
ENDIF(NVCORE_SHARED)

TARGET_LINK_LIBRARIES(nvcore ${LIBS})

# On NetBSD backtrace() is provided by libexecinfo, not libc.
if (CMAKE_SYSTEM_NAME MATCHES "NetBSD")
     TARGET_LINK_LIBRARIES(nvcore execinfo)
endif()

INSTALL(TARGETS nvcore
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/static)
INSTALL(FILES ${CORE_HDRS} DESTINATION include/nvcore )
