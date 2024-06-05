# Contributor: .NET Core Community <https://www.dotnetcore.xyz/>
# Maintainer: Pika Kolendo <pikakolendo02[a]gmail.c0m>

_pkgName="fastgithub"
pkgname="${_pkgName}-bin"
pkgver=2.1.5
pkgrel=1
pkgdesc="Speedup github access in China"
arch=('x86_64')
url="https://github.com/WangGithubUser/FastGitHub"
_url="https://gh-proxy.com/${url}"
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
sha256sums_x86_64=('f4e9caa10bf31f9245610bf5770b26ec8c13eb11337d11bc66bbabc5ddefabf2')
source_aarch64=("${_url}/releases/download/${pkgver}/${_pkgName}_linux-arm64.zip")
sha256sums_aarch64=('f17ffdb8ac34c64cc31a82b5a93ee904c49ba8629e9e968022b5ea4a019754db')
}

[[ "${CHOST}" =~ "-msys" ]] && {
[ "$CARCH" = 'x86_64' ] && _arch='win-x64'
source_x86_64=("${_url}/releases/download/${pkgver}/${_pkgName}_win-x64.zip")
sha256sums_x86_64=('2cdf82209d695788529dcd98ca59e0905d8be5305f4437a8181cb3f4bb736442')
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
