# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-sony-lilac
pkgver=4.4.302
pkgrel=0
pkgdesc="sony Sony Xperia ZX1 Compact kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="sony-lilac"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="android_kernel_sony_msm8998"
_commit="f7d19b10f8cdb038dc0b877f2f557a263f4df34c"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/whatawurst/$_repository/archive/$_commit.tar.gz
	$_config
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
8a8c70013b3e89f38a0f513336a95a5954dcf9a925b15e75713609599c9931abefc65efd6ddb45b74c4708656a026578c60c3eb15244e506bd6ec85a42d93304  linux-sony-lilac-f7d19b10f8cdb038dc0b877f2f557a263f4df34c.tar.gz
5a440e1d8c852d532a7e359eb900eacf3aff60a180478a12f9594fa431bbb388eeb876c618c8fd6df6330213564c765445a0ab95cfca74ad8f9a3fa72a14472b  config-sony-lilac.aarch64
"
