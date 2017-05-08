pkgname=heimdall
pkgver=1.4.1
pkgrel=2
pkgdesc='Tool suite used to flash firmware (aka ROMs) onto Samsung mobile devices'
arch=('x86_64')
url='http://www.glassechidna.com.au/products/heimdall/'
license=('MIT')
depends=('libusb')
optdepends=('android-udev: Udev rules to connect Android devices to your linux box')
source=("heimdall-${pkgver}.tar.gz::https://github.com/Benjamin-Dobell/Heimdall/archive/v${pkgver}.tar.gz"
        )
md5sums=('22c911e9042f5ed8fd90cbeeb9589015'
         )

build() {
  cd Heimdall-$pkgver

  cd libpit/
  ./configure --prefix=/usr
  make

  cd ../heimdall/
  ./configure --prefix=/usr
  make

}

package() {

  cd Heimdall-$pkgver

  # Install license file
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # Install heimdall command line tool
  cd heimdall/

  # Prevent make install from trying to reload udev
  # We'll do this the Arch way at package install time
  mv Makefile Makefile.orig
  sed -e 's/sudo service udev restart/echo sudo service udev restart/' <Makefile.orig >Makefile

  make DESTDIR="$pkgdir" install
  rm -rf "$pkgdir/lib/"

}
