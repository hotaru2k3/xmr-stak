pkgname=xmr-stak
pkgver=2.4.3
pkgrel=1
pkgdesc="Unified All-in-one Monero miner"
arch=('x86_64')
url="https://github.com/fireice-uk/xmr-stak"
license=('GPL3')
makedepends=('git' 'cmake' 'opencl-headers')
depends=('libmicrohttpd' 'openssl' 'hwloc' 'ocl-icd' 'cuda')
source=('git+https://github.com/fireice-uk/xmr-stak.git'
        'xmr-stak.service'
        'no-donate.patch'
	'mesa.patch')
sha256sums=('SKIP'
            '993e6f5e9f6ccdfabe9e2e98776deadc40a718b8b18fc3be15c21310b31762e5'
            'b279c373afbce7cc8610c44f69a5e29a4b36969d131e2fd47229211a3903912a'
            'c55d301dc5ea923c13ff9b15a46ded10806889890ffa6c72ab3395b3383de476')

pkgver() {
    cd "$srcdir/xmr-stak"
    git describe --tags
}

prepare() {
    cd "$srcdir/xmr-stak"
    #patch -p1 -i ../no-donate.patch
    #patch -p1 -i ../mesa.patch
}

build() {
    cd "$srcdir/xmr-stak"
    CC=/bin/gcc-6 CXX=/bin/g++-6 cmake . -DXMR-STAK_COMPILE=generic -DCUDA_ENABLE=OFF
    make
}

package() {
    install -D -m755 "$srcdir/xmr-stak/bin/xmr-stak" -t "$pkgdir/usr/bin/"
    install -D -m644 xmr-stak.service -t "$pkgdir/usr/lib/systemd/system/"
    install -D -m644 "$srcdir/xmr-stak/bin/libxmrstak_cuda_backend.so" -t "$pkgdir/usr/lib"
    install -D -m644 "$srcdir/xmr-stak/bin/libxmrstak_opencl_backend.so" -t "$pkgdir/usr/lib"
}
