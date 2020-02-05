---
layout: post
title:  "Compile socket.io ue4 "
date:   2016-11-29 09:51:02
categories: unrealengine4
---

Test [this project](https://github.com/getnamo/socketio-client-ue4) on Win success.

Need a [android version](https://github.com/getnamo/socketio-client-ue4/issues/21)
 library.

## try to get a android build

seeing [socketio prebuild](https://github.com/getnamo/socketio-client-prebuild)
 to make a andorid prebuild.

## edit project-config.jam
```
using gcc
: arm_linux_android_4.8
: ${ANDROID_NDK_STANDALONE}/bin/arm-linux-androideabi-g++
;
```

## build

```
./b2 \
   -d+2 \
   -j 4 \
   --reconfigure \
   target-os=linux \
   toolset=gcc-arm_linux_android_4.8 \
   include=${ANDROID_NDK_STANDALONE}/include/c++/4.8 \
   link=static \
   variant=release \
   threading=multi \
   --layout=versioned \
   --prefix=~/app/boost \
   install
```

## about v7a v8a x86 x86_64

```shell script
case $ABI in
    armeabi)
        FLAGS="-march=armv5te -mtune=xscale -msoft-float"
        ;;
    armeabi-v7a)
        FLAGS="-march=armv7-a -mfpu=vfpv3-d16 -mfloat-abi=softfp"
        LFLAGS="-Wl,--fix-cortex-a8"
        ;;
    armeabi-v7a-hard)
        FLAGS="-march=armv7-a -mfpu=vfpv3-d16 -mhard-float"
        LFLAGS="-Wl,--fix-cortex-a8"
        LFLAGS="$LFLAGS -Wl,--no-warn-mismatch"
        ;;
    arm64-v8a)
        FLAGS=""
        ;;
    x86)
        FLAGS="-m32"
        ;;
    x86_64)
        FLAGS="-m64"
        ;;
    mips)
        FLAGS="-mabi=32 -mips32"
        ;;
    mips64)
        FLAGS="-mabi=64 -mips64r6"
        ;;
esac
```

nm可以用于查看.a里面的symbol

# 编译for Mac版

一切顺利，已经提交pull request
