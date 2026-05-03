CFLAGS+=" -ffat-lto-objects"

OPTS+=" -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_BUILD_TYPE=None"

cmake  -B build -S . -G Ninja $OPTS &&
cmake --build build &&

prepare_install &&

cmake --install build
