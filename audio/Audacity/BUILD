OPTS+=" -DCMAKE_BUILD_TYPE=Release \
        -DAUDACITY_BUILD_LEVEL=2 \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DSYSCONF_INSTALL_DIR=/etc/audactiy \
        -Daudacity_conan_enabled=OFF \
        -Daudacity_has_crashreports=OFF \
        -Daudacity_has_updates_check=OFF \
        -Daudacity_use_zlib=system \
        -Daudacity_lib_preference=local \
        -Daudacity_obey_system_dependencies=ON \
        -Daudacity_has_vst3=OFF \
        -Daudacity_has_networking=OFF \
        -Daudacity_has_sentry_reporting=OFF \
        -Wno-dev"

export CFLAGS+=" -DNDEBUG"
export CXXFLAGS+=" -DNDEBUG"

cmake -B $MODULE-$VERSION -S . -G Ninja $OPTS &&
cmake --build $MODULE-$VERSION &&

prepare_install &&
cmake --install $MODULE-$VERSION
