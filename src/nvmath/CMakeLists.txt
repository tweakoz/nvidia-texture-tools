PROJECT(nvmath)

SET(MATH_HDRS
    nvmath.h
    Box.h Box.inl
    Color.h Color.inl
    Half.h 
    Matrix.h
    Plane.h Plane.inl 
    SphericalHarmonic.h 
    SimdVector.h SimdVector_SSE.h SimdVector_VE.h
    Vector.h Vector.inl
    Fitting.h 
)

SET(MATH_SRCS
    Fitting.cpp
    Half.cpp
    Plane.cpp
    SphericalHarmonic.cpp)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

# targets
ADD_DEFINITIONS(-DNVMATH_EXPORTS)

IF(NVMATH_SHARED)
    ADD_DEFINITIONS(-DNVMATH_SHARED=1)
    ADD_LIBRARY(nvmath SHARED ${MATH_SRCS})
ELSE(NVMATH_SHARED)
    ADD_LIBRARY(nvmath ${MATH_SRCS})
ENDIF(NVMATH_SHARED)

TARGET_LINK_LIBRARIES(nvmath ${LIBS} nvcore)

INSTALL(TARGETS nvmath
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/static)

INSTALL(FILES ${MATH_HDRS} DESTINATION include/nvmath )
