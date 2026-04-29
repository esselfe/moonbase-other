
python -m build --wheel --skip-dependency-check -C setup-args=-Dblas=blas -C setup-args=-Dlapack=lapack &&

prepare_install
python -m installer --destdir=/ dist/*.whl
