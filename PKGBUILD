# Contributor: .NET Core Community <https://www.dotnetcore.xyz/>
# Maintainer: Pika Kolendo <pikakolendo02[a]gmail.c0m>

_pkgName="fastgithub"
pkgname="${_pkgName}-bin"
pkgver=2.1.4
pkgrel=3
pkgdesc="Speedup github access in China"
arch=('x86_64')
url="https://github.com/dotnetcore/FastGithub"
_url="https://ghproxy.com/${url}"
license=('MIT')
options=('!strip')
provides=('fastgithub')
install="${pkgname}.install"

[[ "${CHOST}" =~ "-linux" ]] && {
arch+=('aarch64')
depends=('mono')
[ "$CARCH" = 'x86_64' ] && _arch='linux-x64'
[ "$CARCH" = 'aarch64' ] && _arch='linux-arm64'
source_x86_64=("${_url}/releases/download/${pkgver}/${_pkgName}_linux-x64.zip")
sha256sums_x86_64=('01106995885a907c5832c594880f79763e6074877e20d61c391b3e9912a3b038')
source_aarch64=("${_url}/releases/download/${pkgver}/${_pkgName}_linux-arm64.zip")
sha256sums_aarch64=('88a54e4c4c3d945f6bb7449804afd0dda3a4c18ef43cc1e8895b38c53484c2a1')
}

[[ "${CHOST}" =~ "-msys" ]] && {
[ "$CARCH" = 'x86_64' ] && _arch='win-x64'
source_x86_64=("${_url}/releases/download/${pkgver}/${_pkgName}_win-x64.zip")
sha256sums_x86_64=('b439afc7b730766aed894876696e9aeb411e3b45f60ebdcfdff247890742c0f6')
}

source+=("${_pkgName}.service")
sha256sums+=('9ad921e57c3aa2c0b87154c52922b19816bc8455cece2921ee8eb340a752bbe7')

prepare() {
[[ "${CHOST}" =~ "-msys" ]] && export MSYS="winsymlinks:lnk"
return 0
}

package() {
    install -dm0755 "${pkgdir}/usr/bin" "${pkgdir}/opt/${pkgname}" "${pkgdir}/usr/lib/systemd/system"
	
    cp -a "${srcdir}/${_pkgName}_${_arch}/"* "${pkgdir}/opt/${pkgname}"
    ln -s "/opt/${pkgname}/${_pkgName}" "${pkgdir}/usr/bin/${_pkgName}"
	install -Dm644 ${srcdir}/${_pkgName}.service ${pkgdir}/usr/lib/systemd/system/
}
