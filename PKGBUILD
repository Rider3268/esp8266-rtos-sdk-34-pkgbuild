# Maintainer: Yurii Shevchuk <yura.shevchuk.02@gmail.com>
pkgname=esp8266-rtos-sdk-34
pkgver=3.4
pkgrel=1
pkgdesc="ESP8266 RTOS SDK v3.4"
arch=('x86_64')
url="https://github.com/espressif/ESP8266_RTOS_SDK"
license=('Espressif MIT')
depends=(python python-click python-pyserial python-cryptography python-pyparsing python-future python-pyelftools ncurses)
optdepends=('xtensa-lx106-elf-gcc-bin: Toolchain for the ESP8266')
makedepends=(gcc gperf)
options=(!strip)
source=("git+https://github.com/espressif/ESP8266_RTOS_SDK#branch=release/v3.4"
	"esp8266-rtos-sdk-34.sh"
	".gitmodules")
sha256sums=('SKIP'
            'SKIP'
	    'SKIP')

prepare() {
	rm ESP8266_RTOS_SDK/.gitmodules
	cp "$srcdir"/.gitmodules ESP8266_RTOS_SDK/
	cd ESP8266_RTOS_SDK

	git submodule init
 	git submodule update --recursive
}

build() {
	# enable 'make menuconfig'
	make -C ESP8266_RTOS_SDK/tools/kconfig
	strip -s ESP8266_RTOS_SDK/tools/kconfig/*conf-idf
	rm -rf ESP8266_RTOS_SDK/tools/kconfig/*.[od]
	rm -rf ESP8266_RTOS_SDK/tools/kconfig/lxdialog/*.[od]
	# tools/ldgen/test has lots of failures
	sed -i -e 's/pyparsing.*/pyparsing/' ESP8266_RTOS_SDK/requirements.txt
}

package() {
	install -d "$pkgdir"/opt/$pkgname
	cp -af ESP8266_RTOS_SDK/* "$pkgdir"/opt/$pkgname
	install -Dm755 "$srcdir"/esp8266-rtos-sdk-34.sh "$pkgdir"/etc/profile.d/esp8266-rtos-sdk-34.sh
}
