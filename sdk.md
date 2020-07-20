## SDK

Собрал 
Протоколирую все действия.
Зависимости OSG.
Зависимости Qt: с какими модулями собирается.

### Репозитарии

### [CadNav](http://www.cadnav.com/3d-models/) Models.zip
  - [AIM120](http://www.cadnav.com/3d-models/model-45973.html)
    Модели можно редактировать в Blender.
  - [Alexander](http://www.cadnav.com/3d-models/model-20980.html)
  - [ClownZombie](http://www.cadnav.com/3d-models/model-40579.html)
  - [Guerilla](http://www.cadnav.com/3d-models/model-40204.html)

### Под вопросом
  - delta3d.zip [Delta3D](https://ru.wikipedia.org/wiki/Delta3D)
    Нет новой версии с 2014 года.
  - ext.zip Какой-то сборник?

### Только для Windows
  - [CMake](https://cmake.org/download/) свежий скачать
  - ms_mpi.zip
  - unzip.zip

### Сборка

* Настройка MPI
```
sudo apt install mpich
sudo update-alternatives --set mpi /usr/bin/mpicc.mpich
```

* Инструменты
```
  flex bison clang-format \
```

* [zlib](http://www.zlib.net/)
```
cd zlib-1.2.11
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [libzip](https://libzip.org/download/)
  [Старая версия](https://github.com/aburgh/libzip)
  libzip.zip
  - zipd нет (отладочная версия? не нужна?)
  - zipconf.h нет
```
cd libzip-1.6.1
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

#### [Boost](https://www.boost.org/users/download/)
  [Installation](https://www.boost.org/doc/libs/1_73_0/more/getting_started/unix-variants.html)
  - (boost_1_72_0_msmpi10.zip)
  - zlib и mpich.
```
./bootstrap.sh --prefix=/tools/root --with-python=python3
```
  - После `./bootstrap.sh` в файл `project-config.jam` добавить `using mpi ;`
```
./b2
./b2 install
```

#### [libTIFF](https://gitlab.com/libtiff/libtiff)
```
git clone https://gitlab.com/libtiff/libtiff.git
cd libtiff && mkdir b && cd b
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make && make install
cd ../..
```

#### [LibPNG](http://www.libpng.org/pub/png/libpng.html)
```
tar xJf libpng-1.6.37.tar.xz
cd libpng-1.6.37/
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [libJPEG](http://www.ijg.org/)
```
tar xzf jpegsrc.v9d.tar.gz
cd jpeg-9d/
./configure --prefix=/tools/root
make -j && make install
```

* [LibXML2](http://xmlsoft.org/downloads.html)
  [github](https://github.com/GNOME/libxml2)
  libxml2.zip
```
git clone https://github.com/GNOME/libxml2.git
cd libxml2
./autogen.sh
./configure --prefix=/tools/root --without-python
make -j && make install
cd ../..
```

* [LibXSLT](http://xmlsoft.org/XSLT/downloads.html)
  [GitLab](https://gitlab.gnome.org/GNOME/libxslt/)
```
git clone https://gitlab.gnome.org/GNOME/libxslt.git
cd libxslt
./autogen.sh --prefix=/tools/root
make -j && make install
```

* [FreeType](https://www.freetype.org/download.html)
  - В `CMakeLists.txt` вставить строку `set(CMAKE_POSITION_INDEPENDENT_CODE ON)`
    [во избежание ошибок](https://stackoverflow.com/questions/38296756/what-is-the-idiomatic-way-in-cmake-to-add-the-fpic-compiler-option)
```
tar xjf freetype-2.10.0.tar.bz2
cd freetype-2.10.0
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make && make install
cd ../..
```

* [GIFLIB](https://sourceforge.net/projects/giflib/files/)
```
tar xzf giflib-5.2.1.tar.gz
cd giflib-5.2.1
# в Makefile: PREFIX=/tools/root
make && make install
```

* [SQLite](https://www.sqlite.org/download.html)
```
cd sqlite-snapshot-202005020408
./configure --prefix=/tools/root
make && make install
cd ../..
```

* [OpenSSL](https://github.com/openssl/openssl/blob/master/INSTALL.md)
```
git clone https://github.com/openssl/openssl.git
cd openssl
./config --prefix=/tools/root
make -j && make install
```

* [cURL](https://curl.haxx.se/)
```
cd curl-7.70.0
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [PROJ](https://proj.org/)
```
cd proj-7.0.1
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [minizip](https://github.com/nmoinvaz/minizip)
```
git clone https://github.com/nmoinvaz/minizip.git
cd minizip
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [GDAL](https://gdal.org/download.html)
  gdal-2.3.0.zip
  - `git clone https://github.com/OSGeo/GDAL.git`
```
git clone https://github.com/OSGeo/gdal.git
cd gdal/gdal
./configure --prefix=/tools/root --with-python=python3 --with-proj=/tools/root --with-libtiff=/tools/root
make -j4 && make install # на много потоков - может память переполниться
cd ../..
```

* [Raptor RDF Syntax Library](http://librdf.org/raptor/)
  [Installation](http://librdf.org/raptor/INSTALL.html)
```
tar xzf raptor2-2.0.15.tar.gz
cd raptor2-2.0.15
./autogen.sh --prefix=/tools/root
make -j && make install
cd ../..

# git clone git://github.com/dajobe/raptor.git
# cd raptor
```

* [FaCT++](https://bitbucket.org/dtsarkov/factplusplus/src/master/)
  [на Google](https://code.google.com/archive/p/factplusplus/)
  fact.zip
  - `git clone https://bitbucket.org/dtsarkov/factplusplus.git`

* [owl-cpp](http://owl-cpp.sourceforge.net/)
  - Не понятно, как собирать
  - Не критично
```
tar xjf owlcpp-v0.3.4.tar.bz2
cd owlcpp-v0.3.4
```

* [ColladaDOM3](https://www.khronos.org/collada/wiki/ColladaDOM_3)
  [Collada-DOM](https://github.com/rdiankov/collada-dom)
  collada-dom-2.5.1.zip
```
git clone https://github.com/rdiankov/collada-dom.git
cd collada-dom
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [SDL2](https://www.libsdl.org/download-2.0.php)
  SDL2-2.0.5.zip
  - [Tutorial](https://chebykin.org/simple-sdl-opengl-program-tutorial)
```
tar xzf SDL2-2.0.12.tar.gz
cd SDL2-2.0.12
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [OpenEXR](https://www.openexr.com/downloads.html)
```
git clone https://github.com/AcademySoftwareFoundation/openexr.git
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [JasPer](https://www.ece.uvic.ca/~frodo/jasper/)
```
git clone https://github.com/mdadams/jasper.git
```

* [FFmpeg](http://www.ffmpeg.org/download.html#get-sources)
```
git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg
```

* [OSG](https://github.com/openscenegraph/OpenSceneGraph)
  osg-3.6.3.zip
  - [Зависимости - osg-3rdparty-cmake](https://github.com/bjornblissing/osg-3rdparty-cmake)
  - [Tutorial](https://habr.com/ru/post/429816/)
  - [Getting started](http://www.openscenegraph.org/index.php/documentation/getting-started)
```
git clone https://github.com/openscenegraph/OpenSceneGraph.git
cd OpenSceneGraph
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [GFLAGS](https://github.com/gflags/gflags)
```
git clone https://github.com/gflags/gflags.git
cd gflags
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [RocksDB](https://github.com/facebook/rocksdb)
```
git clone https://github.com/facebook/rocksdb.git
cd rocksdb
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j4 && make install
cd ../..
```

* [GLEW](http://glew.sourceforge.net/)
```
git clone https://github.com/nigels-com/glew.git glew
```

* [OSG Earth](https://github.com/gwaldron/osgearth)
  osgearth-2.10.zip
```
git clone https://github.com/gwaldron/osgearth.git
cd osgearth
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

* [Qt](https://wiki.qt.io/Building_Qt_5_from_Git#Getting_the_source_code)
  qt.zip
```
git clone https://code.qt.io/qt/qt5.git
cd qt5/
perl init-repository
./configure -developer-build -opensource --prefix=/tools/root
```

* [SOCI](https://github.com/SOCI/soci)
  soci-pq-9.5.zip
```
git clone https://github.com/SOCI/soci.git
cd soci
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/tools/root ..
make -j && make install
cd ../..
```

