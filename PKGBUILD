pkgname=emby-server
<<<<<<< HEAD
pkgver=3.0.5818
=======
pkgver=3.0.5782.0
>>>>>>> a730bf1ede41419a652338bde94fe291cbd8f303
pkgrel=1
pkgdesc='Bring together your videos, music, photos, and live television'
arch=('x86_64')
url='http://emby.media'
license=('GPL2')
depends=('ffmpeg' 'imagemagick' 'libmediainfo' 'mono' 'sqlite')
install='emby-server.install'
source=("emby-server-${pkgver}.tar.gz::https://github.com/MediaBrowser/MediaBrowser/archive/${pkgver}.tar.gz"
        'emby-server'
        'emby-migrate-database'
        'emby-server.conf'
        'emby-server.service')
backup=('etc/conf.d/emby-server')
<<<<<<< HEAD
sha256sums=('8530117373e9a7fb2a11bdae968469b553953cb5c3eacb6b0acc96b338250691'
=======
sha256sums=('08a23bdf0b0f609abf960374e53a144bcec63c55367915072e6f668fbbec6cda'
>>>>>>> a730bf1ede41419a652338bde94fe291cbd8f303
            '7b1974f7bba8ac4b76e51ef7fe1257d165c7c4abbd0915e192391336048a3d74'
            '0e3f6b7fe700a3bbdf97bdae8655453b34b1bd08fa8ae339e0fd130fe8670b0b'
            'c9ad78f3e2f0ffcb4ee66bb3e99249fcd283dc9fee17895b9265dc733288b953'
            '8a91ea49a1699c820c4a180710072cba1d6d5c10e45df97477ff6a898f4e1d70')

prepare() {
  cd Emby-${pkgver}

  sed 's/libMagickWand-6.Q8.so/libMagickWand-6.Q16HDRI.so/' -i MediaBrowser.Server.Mono/ImageMagickSharp.dll.config
}

build() {
  cd Emby-${pkgver}

  xbuild \
    /p:Configuration='Release Mono' \
    /p:Platform='Any CPU' \
    /p:OutputPath="${srcdir}/build" \
    /t:build MediaBrowser.Mono.sln
}

package() {
  install -dm 755 "${pkgdir}"/{etc/conf.d,usr/{bin,lib/systemd/system}}
  cp -dr --no-preserve='ownership' build "${pkgdir}"/usr/lib/emby-server
  install -m 755 emby-server "${pkgdir}"/usr/bin/
  install -m 755 emby-migrate-database "${pkgdir}"/usr/bin/
  install -m 644 emby-server.service "${pkgdir}"/usr/lib/systemd/system/
  install -m 644 emby-server.conf "${pkgdir}"/etc/conf.d/emby-server

  install -dm 755 "${pkgdir}"/var/lib/emby
  chown 422:422 -R "${pkgdir}"/var/lib/emby
}

# vim: ts=2 sw=2 et:

