# Maintainer: zhullyb <zhullyb [at] outlook dot com>

pkgname=com.antutu.benchmark
pkgver=1.0.0.591
pkgrel=3
pkgdesc="安兔兔评测 for linux
 安兔兔评测（AnTuTu）是一款跨平台，支持手机、电脑设备的专业性能评定软件。Linux 版本的安兔兔支持一键跑分，可评估 CPU/GPU/MEM/UX 性能。"
arch=("x86_64")
url="https://www.antutu.com/"
license=("custom")
depends=()
options=(!strip)
provides=('antutu')
source=("http://file.antutu.com/soft/com.antutu.benchmark_amd64.deb"
        "fix-desktop-paths.patch")
md5sums=('f114e5fe49ad569a5ce412247a72644e'
         'SKIP')

prepare(){
    cd ${srcdir}
    tar -xvf data.tar.zst -C "${srcdir}"
    
    # Apply patch to fix desktop file paths
    patch -p1 < "${srcdir}/fix-desktop-paths.patch"
}

package(){
    cd ${srcdir}

    mkdir -p ${pkgdir}/opt/antutu
    mv opt/apps/${pkgname}/files/* ${pkgdir}/opt/antutu/

    mkdir -p ${pkgdir}/usr/share/
    mv opt/apps/${pkgname}/entries/*  ${pkgdir}/usr/share/

    echo '''#!/bin/bash

export LD_LIBRARY_PATH=/opt/antutu:$LD_LIBRARY_PATH
export LANG=en_US.UTF-8
/opt/antutu/bin/benchmark -start $1
''' >  ${pkgdir}/opt/antutu/start.sh
    chmod a+x ${pkgdir}/opt/antutu/start.sh
    mkdir -p ${pkgdir}/usr/bin
    ln -s /opt/antutu/start.sh ${pkgdir}/usr/bin/antutu
}
