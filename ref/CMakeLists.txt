
cmake_minimum_required(VERSION 3.6)
project(kyber)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall")

find_package(OPENSSL REQUIRED)
include_directories(${OPENSSL_INCLUDE_DIR})

set(SOURCES kem.c poly.c polyvec.c reduce.c cbd.c ntt.c verify.c indcpa.c)
set(SOURCESKECCAK ${SOURCES} fips202.c symmetric-fips202.c)
set(SOURCESNINETIES ${SOURCES} sha256.c sha512.c aes256ctr.c)
set(HEADERS params.h poly.h polyvec.h reduce.h cbd.h ntt.h verify.h indcpa.h)
set(HEADERSKECCAK ${HEADERS} fips202.h)
set(HEADERSNINETIES ${HEADERS} aes256ctr.h sha2.h)

add_executable(PQCgenKAT_kem ${SOURCESKECCAK} ${HEADERSKECCAK} PQCgenKAT_kem.c rng.h rng.c)
target_link_libraries(PQCgenKAT_kem ${OPENSSL_CRYPTO_LIBRARY})
