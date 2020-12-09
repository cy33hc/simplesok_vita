cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

include("$ENV{DOLCESDK}/share/dolce.toolchain.cmake" REQUIRED)
include("$ENV{DOLCESDK}/share/dolce.cmake" REQUIRED)
set(DOLCE_APP_NAME "sokoban")
set(DOLCE_TITLEID  "SMLA00002")
set(DOLCE_VERSION  "01.00")
set(DOLCE_MKSFOEX_FLAGS "${DOLCE_MKSFOEX_FLAGS} -d PARENTAL_LEVEL=1")
set(DOLCE_ELF_CREATE_FLAGS "${DOLCE_ELF_CREATE_FLAGS} -h 4194304")

project(sokoban)

include(CheckCXXCompilerFlag)
include(GNUInstallDirs)


include_directories(
  ${sokoban_SOURCE_DIR}
)

add_definitions("-Wall")

add_executable(${PROJECT_NAME}
  crc32.c
  gz.c
  net.c
  save.c
  sok.c
  sok_core.c
)

target_link_libraries(${PROJECT_NAME}
  SceDisplay_stub
  SceCtrl_stub
  SceAppMgr_stub
  SceAudio_stub
  SceSysmodule_stub
  SceSharedFb_stub
  SceDisplay_stub
  SceDisplayUser_stub
  SceCtrl_stub
  SceAppMgr_stub
  SceAppMgrUser_stub
  SceAudio_stub
  SceIofilemgr_stub
  SceSysmodule_stub
  SceGxm_stub
  SceGxmInternalForVsh_stub
  SceCommonDialog_stub
  SceTouch_stub
  SceHid_stub
  SceMotion_stub
  SDL2
  SDL2_image
  png
  jpeg
  pib
  m
  z
  FLAC
  vorbisfile
  vorbis
  ogg
  mikmod
  mpg123
)

dolce_create_self(${PROJECT_NAME}.self ${PROJECT_NAME} UNSAFE)
dolce_create_vpk(${PROJECT_NAME}.vpk ${DOLCE_TITLEID} ${PROJECT_NAME}.self
  VERSION ${DOLCE_VERSION}
  NAME ${DOLCE_APP_NAME}
)
