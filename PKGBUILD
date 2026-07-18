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
if [[ "${_os}" == "Android" ]]; then
  _compiler="clang"
  _libc="ndk-sysroot"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _compiler="gcc"
  _libc="glibc"
elif [[ "${_os}" == "Windows" ]]; then
  _compiler="gcc"
  _libc="glibc"
fi
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
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
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
if [[ ! -v "_ns" ]]; then
  _ns="${_kernel}-${_pkg}"
  _ns="themartiancompany"
fi
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
  "${_compiler}"
  "flex"
  "make"
  'shadow'
  'w3m'
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "docbook-xml>=${_docbook_xml_pkgver}"
    "docbook-xsl"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
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
if [[ "${_tag_name}" == "pkgver" ]]; then
  _tag="${pkgver}"
elif [[ "${_tag_name}" == "commit" ]]; then
  _tag="${_commit}"
fi
_tarname="${_Kernel}-${_PKG}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_http="https://${_git_service}.com"
_url="${_http}/${_ns}/${_kernel}-${_pkg}"
_evmfs_ns="0x836339402ccb4Bb2bb2051Feb3d1aDC697381B7C"
_chain_id="100"
_fs="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_bundle_sum="0abc2b686259be9a1e3bd70b29d965faa1e461b1c99b8256aa6a2e99a56d0e5a"
_bundle_sig_sum="fae6c7f6a1ae8dfc112c0dfcb9a1acf22962996b236b0e6e112fc428e81b8c9a"
_pkgver_sum="fff4a34e5bbee77e2e8f1992f27631e2329bcbf8a0563ddeb5c3389b4e3169ad"
_pgkver_sig_sum="SKIP"
_docs_pkgver_sum="3e82730d3350795c42f3708f6609a92c1df841d518aa17c28fd702fe5ec23a32"
_docs_pkgver_sig_sum="SKIP"
_evmfs_dir="evmfs://${_chain_id}/${_fs}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_bundle_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_bundle_sig_sum}"
_sig_src="${_tarfile}::${_sig_uri}"
source=(
  "${pkgname}.tmpfiles"
)
sha256sums=(
  '5631f224e90c4f0459361c2a5b250112e3a91ba849754bb6f67d69d683a2e5ac'
)
if [[ "${_evmfs}" == "false" ]]; then
  source+=(
    "${_url}/releases/download/v${pkgver}/${_tarname}"{"","-docs"}".tar.xz"{"",".asc"}
  )
  validpgpkeys=(
    # Thorsten Kukuk
    '8C6BFD92EE0F42EDF91A6A736D1A7F052E5924BB'
    # Dimitry V. Levin
    #   <ldv@altlinux.org>
    '296D6F29A020808E8717A8842DB5BD89A340AEB7'
  )
  _sum="${_pkgver_sum}"
  _sig_sum="SKIP"
  _docs_sum="${_docs_pkgver_sum}"
  _docs_sig_sum="${_docs_pkgver_sig_sum}"
  sha256sums+=(
    "${_sum}"
    "${_sig_sum}"
    "${_docs_sum}"
    "${_docs_sig_sum}"
  )
elif [[ "${_evmfs}" == "true" ]]; then
  _sum="${_bundle_sum}"
  _sig_sum="${_bundle_sig_sum}"
  validpgpkeys=(
    # Truocolo
    #   <truocolo@aol.com>
    '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
    #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
    'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
    # Pellegrino Prevete (dvorak)
    #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
    '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
  )
  source+=(
    "${_evmfs_src}"
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sum}"
    "${_sig_sum}"
  )
fi
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
