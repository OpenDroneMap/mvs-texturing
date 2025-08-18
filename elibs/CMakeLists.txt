externalproject_add(ext_mapmap
    PREFIX          ext_mapmap
    GIT_REPOSITORY  https://github.com/dthuerck/mapmap_cpu
    GIT_TAG         fa526e0963ca3e431a02aa7b9e87b85ba8a8e304
    UPDATE_COMMAND  ""
    SOURCE_DIR      ${CMAKE_SOURCE_DIR}/elibs/mapmap
    CONFIGURE_COMMAND ""
    BUILD_COMMAND   ""
    INSTALL_COMMAND ""
)

externalproject_add(ext_rayint
    PREFIX          ext_rayint
    GIT_REPOSITORY  https://github.com/pierotofy/rayint.git
    GIT_TAG         cuda
    UPDATE_COMMAND  ""
    SOURCE_DIR      ${CMAKE_SOURCE_DIR}/elibs/rayint
    CONFIGURE_COMMAND ""
    BUILD_COMMAND   ""
    INSTALL_COMMAND ""
)

externalproject_add(ext_eigen
    PREFIX          ext_eigen
    URL             https://gitlab.com/libeigen/eigen/-/archive/3.3.2/eigen-3.3.2.tar.gz
    URL_MD5         02edfeec591ae09848223d622700a10b
    SOURCE_DIR      ${CMAKE_SOURCE_DIR}/elibs/eigen
    CONFIGURE_COMMAND ""
    BUILD_COMMAND   ""
    INSTALL_COMMAND ""
)
