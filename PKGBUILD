# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: judd <jvinet@zeroflux.org>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>

pkgname=pam
pkgver=1.6.0
pkgrel=3
pkgdesc="PAM (Pluggable Authentication Modules) library"
arch=(
  'x86_64'
  'arm'
)
license=('GPL2')
url="http://linux-pam.org"
depends=(
  'glibc'
  'libtirpc'
  'pambase'
  'audit'
  'libaudit.so'
  'libxcrypt'
  'libcrypt.so'
)
makedepends=(
  'flex'
  'w3m'
  'docbook-xml>=4.4'
  'docbook-xsl'
  'shadow'
)
provides=(
  'libpam.so'
  'libpamc.so'
  'libpam_misc.so')
backup=(etc/security/{access.conf,faillock.conf,group.conf,limits.conf,namespace.conf,namespace.init,pwhistory.conf,pam_env.conf,time.conf} etc/environment)
source=(https://github.com/linux-pam/linux-pam/releases/download/v$pkgver/Linux-PAM-$pkgver{,-docs}.tar.xz{,.asc}
        $pkgname.tmpfiles)
validpgpkeys=(
        '8C6BFD92EE0F42EDF91A6A736D1A7F052E5924BB' # Thorsten Kukuk
        '296D6F29A020808E8717A8842DB5BD89A340AEB7' #Dimitry V. Levin <ldv@altlinux.org>
)

sha256sums=(
  'fff4a34e5bbee77e2e8f1992f27631e2329bcbf8a0563ddeb5c3389b4e3169ad'
  'SKIP'
  '3e82730d3350795c42f3708f6609a92c1df841d518aa17c28fd702fe5ec23a32'
  'SKIP'
  '5631f224e90c4f0459361c2a5b250112e3a91ba849754bb6f67d69d683a2e5ac'
)
options=(
  '!emptydirs'
)

build() {
  local \
    _configure_opts=()
  _configure_opts=(
    --libdir=/usr/lib
    --sbindir=/usr/bin
    --disable-db
  )
  [[ "${_systemd}" == true ]] && \
    _configure_opts+=(
      --enaable-logind
    )
  [[ "${_systemd}" == false ]] && \
    _configure_opts+=(
      --disable-logind
    )
  cd Linux-PAM-$pkgver
  ./configure \
    "${_configure_opts[@]}"
  make
}

package() {
  install \
    -Dm 644 \
    $pkgname.tmpfiles \
    "$pkgdir"/usr/lib/tmpfiles.d/$pkgname.conf
  cd \
    Linux-PAM-$pkgver
  make \
    DESTDIR="$pkgdir" \
    SCONFIGDIR=/etc/security install

  # set unix_chkpwd uid
  chmod +s "$pkgdir"/usr/bin/unix_chkpwd
}

# vim: ft=sh syn=sh et
