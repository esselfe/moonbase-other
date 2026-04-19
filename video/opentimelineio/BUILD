git submodule init src/deps/rapidjson &&
git submodule set-url src/deps/rapidjson opentimelineio-rapidjson &&
git -c protocol.file.allow=always submodule update src/deps/rapidjson &&

sed -e '/cmake/d' -i pyproject.toml &&

OPTS+=" -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_BUILD_TYPE=Release \
        -DOTIO_FIND_IMATH=ON \
        -DOTIO_AUTOMATIC_SUBMODULES=OFF \
        -DOTIO_DEPENDENCIES_INSTALL=OFF \
        -Wno-dev"

cmake -B $MODULE-$VERSION -S . -G Ninja $OPTS &&
cmake --build $MODULE-$VERSION &&

export CXXFLAGS+=" -I/usr/include/Imath"
python -m build --wheel --no-isolation &&

prepare_install
cmake --install $MODULE-$VERSION &&
python -m installer --destdir=/ dist/*.whl
