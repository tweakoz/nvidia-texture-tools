PROJECT(nvthread)

SET(THREAD_SRCS
	nvthread.h nvthread.cpp
	Atomic.h
	Event.h Event.cpp
	Mutex.h Mutex.cpp
	ParallelFor.h ParallelFor.cpp
	Thread.h Thread.cpp
	ThreadPool.h ThreadPool.cpp)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

# targets
ADD_DEFINITIONS(-DNVTHREAD_EXPORTS)

ADD_LIBRARY(nvthread SHARED ${THREAD_SRCS})

TARGET_LINK_LIBRARIES(nvthread ${LIBS} nvcore)

INSTALL(TARGETS nvthread
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	)
