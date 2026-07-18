# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Tobias Powalowski
#     <tpowa@archlinux.org>
#   Levente Polyak
#     <anthraxx[at]archlinux[dot]org>
#   judd
#     <jvinet@zeroflux.org>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_evmfs}" == "false" ]]; then
    _git="false"
  elif [[ "${_evmfs}" == "true" ]]; then
    _git="true"
  fi
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _tag_name="pkgver"
  elif [[ "${_git}" == "true" ]]; then
    _tag_name="commit"
  fi
fi
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
elif [[ "${_os}" == "Windows" ]]; then
  _libc="glibc"
fi
_pkg=pam
_PKG=PAM
_kernel=linux
_Kernel=Linux
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=1.6.0
_docbook_xml_pkgver="4.4"
_bundle_commit="fe03a10115c082a8486ccbab7462139d7e4bb067"
_commit="${_bundle_commit}"
pkgrel=3
_pkgdesc=(
  "${_PKG} (Pluggable"
  "Authentication Modules)"
  "library"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  "aarch64"
  "arm"
  "armv8l"
  "armv7l"
  "armv6l"
  "i686"
  "mips"
  "pentium4"
  "powerpc"
  'x86_64'
)
license=(
  'GPL2'
)
url="http://${_kernel}-${_pkg}.org"
depends=(
  'audit'
  "${_libc}"
  'libtirpc'
  "${_pkg}base"
  "libaudit.so"
  "libxcrypt"
  "libcrypt.so"
)
makedepends=(
  "flex"
  'shadow'
  'w3m'
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "docbook-xml>=${_docbook_xml_pkgver}"
    "docbook-xsl"
  )
fi
provides=(
  "lib${_pkg}.so"
  "lib${_pkg}c.so"
  "lib${_pkg}_misc.so"
)
backup=(
  "etc/security/"{"access.conf","faillock.conf","group.conf","limits.conf","namespace.conf","namespace.init","pwhistory.conf","${_pkg}_env.conf","time.conf"} \
  "etc/environment"
)
_http="https://github.com"
_ns="${_kernel}-${_pkg}"
_url="${_http}/${_ns}/${_kernel}-${_pkg}"
_evmfs_ns="0x836339402ccb4Bb2bb2051Feb3d1aDC697381B7C"
_bundle_sum="0abc2b686259be9a1e3bd70b29d965faa1e461b1c99b8256aa6a2e99a56d0e5a"
_bundle_sig_sum="fae6c7f6a1ae8dfc112c0dfcb9a1acf22962996b236b0e6e112fc428e81b8c9a"
source=(
  "${_url}/releases/download/v$pkgver/${_Kernel}-${_PKG}-${pkgver}"{"","-docs"}".tar.xz"{"",".asc"}
  "${pkgname}.tmpfiles"
)
validpgpkeys=(
  # Thorsten Kukuk
  '8C6BFD92EE0F42EDF91A6A736D1A7F052E5924BB'
  # Dimitry V. Levin
  #   <ldv@altlinux.org>
  '296D6F29A020808E8717A8842DB5BD89A340AEB7'
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
    --libdir="/usr/lib"
    --sbindir="/usr/bin"
    --disable-db
  )
  if [[ "${_systemd}" == true ]]; then
    _configure_opts+=(
      --enable-logind
    )
  elif [[ "${_systemd}" == false ]]; then
    _configure_opts+=(
      --disable-logind
    )
  fi
  cd \
    "${_Kernel}-${_PKG}-${_tag}"
  ./configure \
    "${_configure_opts[@]}"
  make
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
    SCONFIGDIR="/etc/security"
  )
  install \
    -vDm644 \
    "${pkgname}.tmpfiles" \
    "${pkgdir}/usr/lib/tmpfiles.d/${_pkg}.conf"
  cd \
    "${_Kernel}_${_PKG}-${pkgver}"
  make \
    "${_make_opts[@]}" \
    install
  # set unix_chkpwd uid
  chmod \
    +s \
    "${pkgdir}/usr/bin/unix_chkpwd"
}

# vim: ft=sh syn=sh et
