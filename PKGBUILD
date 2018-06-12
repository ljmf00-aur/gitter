# Maintainer: Tomas Ostasevicius (aquarix) <t dot ostasevicius at gmail dot com>
pkgname=gitter
pkgver=4.0.0
pkgrel=4
pkgdesc='Where developers come to talk'
url='https://gitlab.com/gitlab-org/gitter/desktop/'
license=('MIT')
arch=('x86_64' 'i686')
depends=('libsystemd' 'desktop-file-utils' 'gconf' 'gtk2' 'alsa-lib' 'nss'
'libnotify' 'libxtst')
makedepends=('tar' 'binutils')
source_x86_64=("https://update.gitter.im/linux64/${pkgname}_${pkgver}_amd64.deb"
        gitter_x86_64.sh)
source_i686=("https://update.gitter.im/linux32/${pkgname}_${pkgver}_i386.deb"
        gitter_i686.sh)
noextract=("${pkgname}_${pkgver}_amd64.deb" "${pkgname}_${pkgver}_i386.deb")
install='gitter.install'
sha256sums_i686=('96afabafbd4d189227f999da022e264bd99980e9401591c8e02b501aa9a1def4'
         'c29fbff9e3ad766c49407cb29aa5ba7131f4de9f48c71928ffcf8b3bcd2a2cde')
sha256sums_x86_64=('56d20b1accd141f7d548ac3afd763407ca3bef72f6358919ae33c1377576a0a5'
         'f791f6685771517b2e7ab03513fc49f625cb9feab4949b607b444e303f31fab5')
options=(!strip)

prepare() {
  cd "$srcdir"
  if [ "$CARCH" == "x86_64" ]; then
    ar x "${pkgname}_${pkgver}_amd64.deb"
  else
    ar x "${pkgname}_${pkgver}_i386.deb"
  fi
}

package() {
  cd "$srcdir"
  tar -C "$pkgdir" -xf data.tar.gz
  mkdir -p "$pkgdir/opt/Gitter/lib"
  ln -sf /usr/lib/libudev.so.1 "$pkgdir/opt/Gitter/lib/libudev.so.0"
  if [ "$CARCH" == "x86_64" ]; then
	  install -Dm755 "$srcdir/${pkgname}_x86_64.sh" "$pkgdir/usr/bin/$pkgname"
	  RPM_BUILD_ROOT="$pkgdir" desktop-file-install "$pkgdir/opt/Gitter/linux64/gitter.desktop"
	  sed -e 's#/opt/Gitter/linux64/Gitter#/usr/bin/gitter#' -i "$pkgdir/usr/share/applications/gitter.desktop"
  else
	  install -Dm755 "$srcdir/${pkgname}_i686.sh" "$pkgdir/usr/bin/$pkgname"
	  RPM_BUILD_ROOT="$pkgdir" desktop-file-install "$pkgdir/opt/Gitter/linux32/gitter.desktop"
	  sed -e 's#/opt/Gitter/linux32/Gitter#/usr/bin/gitter#' -i "$pkgdir/usr/share/applications/gitter.desktop"
  fi
}
