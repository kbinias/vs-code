# Obtaining Gperftools and using it in paddle

## Build and install
Build gperftools from source and install locally
```
git clone --depth=1 https://github.com/linux-on-ibm-z/gperftools.git
cd gperftools
./autogen.sh
./configure --prefix ~/.local/
make -j8
make install
```

## Build paddle using local gperftools

Modify {PADDLE_ROOT}/cmake/FindGperftools.cmake

by adding following instruction to the beginning of the file
```cmake
set(Gperftools_ROOT_DIR <your_home_dir>/.local/)
```
