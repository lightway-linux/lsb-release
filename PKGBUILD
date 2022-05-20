# Maintainer: Jonas Witschel <diabonas@archlinux.org>
# Contributor: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Malte Rabenseifner <malte@zearan.de>
# Contributor: John Gerritse <reaphsharc@gmail.com>

pkgname=lsb-release
pkgver=2.0.r48.3cf5103
_commit=3cf51039933d03ef15388b75d30baa5d5e09a1a0
pkgrel=1
pkgdesc="LSB version query program"
arch=('any')
url="https://refspecs.linuxfoundation.org/lsb.shtml"
license=('GPL')
depends=('sh')
makedepends=('git')
source=("git+https://github.com/LinuxStandardBase/lsb-samples.git#commit=$_commit"
        'lsb-release'
        'lsb_release_description.patch'
        'lsb_release_make_man_page_reproducible.patch')
sha512sums=('SKIP'
            'ee69ad9c344abd74f701ab5a2b651716d3416b5d0ad3445deb7ee0cffbd04e1e6651894f56bc2f16920976c17d92ec6c6f112f26552ac6d6840fd6c3f508ef88'
            '145ef64f90f5e6cc59075679e640cf7c1ad02617c12eff17f10b05c1cc219591fdba1b27be2b2c8480742aed24ce81d6a7badcbaca6772faea4ebc6a55695b62'
            'ab64a1d236d00a30a48e3af2c5bdfa0aad0183ebe0df4f2b0c6af58530c2a1fdac1b0a5cdd8a1800d5f8405f44562603cddf28eb318b5badaabd49a82e0b7e83')

pkgver() {
	cd lsb-samples/lsb_release/src
	printf "%s.r%s.%s" "$(grep -Po 'SCRIPTVERSION="\K[^"]*' lsb_release)" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd lsb-samples/lsb_release/src
	patch -Np0 -i "$srcdir/lsb_release_description.patch"
	patch -Np1 -i "$srcdir/lsb_release_make_man_page_reproducible.patch"
}

build() {
	cd lsb-samples/lsb_release/src
	make
}

package() {
	cd lsb-samples/lsb_release/src
	install -Dm644 lsb_release.1.gz -t "$pkgdir/usr/share/man/man1"
	install -Dm755 lsb_release -t "$pkgdir/usr/bin"
	install -Dm644 "$srcdir/lsb-release" -t "$pkgdir/etc"
}
