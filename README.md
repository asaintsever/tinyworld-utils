# Utils for TinyWorld

## JRE distros

Supported JRE distributions are stored in [Release](https://github.com/asaintsever/tinyworld-utils/releases). They are used to build the portable and AppImage packages of TinyWorld.

## ImageMagick with HEIF/HEIC support

Linux x64/arm64 and Windows x64 static binaries of ImageMagick 7.1.0 with HEIF/HEIC support can be found in [Release](https://github.com/asaintsever/tinyworld-utils/releases) section.

Currently, TinyWorld only relies on ImageMagick for thumbnails generation from HEIF photos.

### Linux build

Linux binary has been compiled from source as existing packages do not come with HEIC support.

Instructions to build static binary:

```sh
# Install libs for HEIF (HEIC) support
$ sudo apt install libjpeg-dev libheif-dev libheif1

# Clone latest tag
$ git clone --depth 1 --branch 7.1.0-46 https://github.com/ImageMagick/ImageMagick.git
$ cd ImageMagick

# Configure build to generate static binaries. Enable HEIC support
$ ./configure --enable-static=yes --enable-shared=no --prefix=/usr --with-jpeg=yes --with-heic=yes --without-magick-plus-plus --without-perl --with-quantum-depth=16

# Compile
$ make

# Install in a temporary folder
$ mkdir -p /tmp/MyIM
$ make install DESTDIR=/tmp/MyIM

# Check HEIC support is enabled
# Make sure both 'jpeg' and 'heic' are listed in 'Delegates (built-in)'
$ cd /tmp/MyIM/usr/bin
$ ./magick -version
Version: ImageMagick 7.1.0-46 Q16-HDRI x86_64 5ef3d4d66:20220816 https://imagemagick.org
Copyright: (C) 1999 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC HDRI OpenMP(4.5)
Delegates (built-in): bzlib djvu fontconfig freetype gvc heic jbig jng jpeg lcms lqr lzma openexr pangocairo png raqm raw tiff webp x zip zlib
Compiler: gcc (11.2)
```

### Generate thumbnail from HEIF photo

```sh
# Generate a 160x160 thumbnail
magick <your HEIF file> -thumbnail 160x160 jpg:<your thumbnail name>.jpg
```

## WorlWind Cache for TinyWorld

This repo hosts a [NASA WorldWind](https://worldwind.arc.nasa.gov/java/) cache to use as a starter on any WorldWind-based application, e.g. **[TinyWorld](https://github.com/asaintsever/tinyworld)**. It helps to get first tiles, all the most if you don't have a good Internet connection.

> The cache is available for several tiles format:
> - DDS
> - JPEG and PNG (depends on the layer)
> 
> For each layer, tiles format is defined via the `ImageFormat` tag in the corresponding layer's config file (e.g. of layers' config files: `Earth/BMNGWMSLayer2.xml`, `Earth/LandsatI3WMSLayer2.xml`).

The data is provided compressed in the [Release](https://github.com/asaintsever/tinyworld-utils/releases) section.
