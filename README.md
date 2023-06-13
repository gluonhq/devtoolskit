# devtoolskit

Creating a devkit to build the other tools/products.

## Building

Use the provided Makefile to build the devkit:

    cd make/devkit
    make tars BASE_OS=OL

## Finalizing

After the build has completed, the following extra steps need to be executed:

  - add `pkg-config`

        cd build/devkit/result/x86_64-linux-gnu-to-x86_64-linux-gnu
        cp /usr/bin/pkg-config bin/

  - link extra include directories

        cd x86_64-linux-gnu/sysroot/usr/include
        ln -s /usr/include/x86_64-linux-gnu/libavcodec
        ln -s /usr/include/x86_64-linux-gnu/libavutil
        ln -s /usr/include/x86_64-linux-gnu/libswscale
        ln -s /usr/include/x86_64-linux-gnu/libavformat
        cp /usr/include/linux/videodev2.h linux/

## Using

To use the devkit, the following environment variables should be set:

    PKG_CONFIG_SYSROOT_DIR=/home/ubuntu/devtoolskit/build/devkit/result/x86_64-linux-gnu-to-x86_64-linux-gnu/x86_64-linux-gnu/sysroot
    PKG_CONFIG_PATH=${PKG_CONFIG_SYSROOT_DIR}/usr/lib64/pkgconfig:${PKG_CONFIG_SYSROOT_DIR}/usr/share/pkgconfig
    PKG_CONFIG_ALLOW_SYSTEM_CFLAGS=1
