pkgname=xmr-stak-nogpu
pkgver=2.4.3
pkgrel=1
pkgdesc="Unified All-in-one Monero miner"
arch=('x86_64')
url="https://github.com/fireice-uk/xmr-stak"
license=('GPL3')
makedepends=('git' 'cmake' 'opencl-headers')
depends=('libmicrohttpd' 'openssl' 'hwloc')
source=('git+https://github.com/fireice-uk/xmr-stak.git'
        'xmr-stak.service'
        'no-donate.patch')
sha256sums=('SKIP'
            'd2fafff6c85bbb30f111e813ad856ddacf6111af2c5d05e604f209fea7f9b447'
            'b279c373afbce7cc8610c44f69a5e29a4b36969d131e2fd47229211a3903912a')

pkgver() {
    cd "$srcdir/xmr-stak"
    git describe --tags
}

prepare() {
    cd "$srcdir/xmr-stak"
    #patch -p1 -i ../no-donate.patch
}

build() {
    cd "$srcdir/xmr-stak"
    CC=/bin/gcc-6 CXX=/bin/g++-6 cmake . -DXMR-STAK_COMPILE=generic -DOpenCL_ENABLE=OFF -DCUDA_ENABLE=OFF
    make
}

package() {
    install -D -m755 "$srcdir/xmr-stak/bin/xmr-stak" -t "$pkgdir/usr/bin/"
    install -D -m644 xmr-stak.service -t "$pkgdir/usr/lib/systemd/system/"
    #install -D -m644 "$srcdir/xmr-stak/bin/libxmrstak_cuda_backend.so" -t "$pkgdir/usr/lib"
    #install -D -m644 "$srcdir/xmr-stak/bin/libxmrstak_opencl_backend.so" -t "$pkgdir/usr/lib"
}
