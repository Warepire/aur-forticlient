pkgname=forticlient
pkgver=6.0.8.0140
pkgrel=1
pkgdesc="FortiClient"
arch=("x86_64")
url="https://www.fortinet.com"
license=('custom')
# Their own electron is broken, use the system one
# It claims to have a dep on libappindicator-gtk2, but at least with AwesomeWM
# having that installed makes FortiClient hang and never finish init.
depends=('electron2')
makedepends=('rsync')
provides=(forticlient)
source=("https://repo.fortinet.com/repo/ubuntu/pool/multiverse/${pkgname}/${pkgname}_${pkgver}_amd64.deb"
	"FortiClient")
noextract=()
sha256sums=('d6667104f4c2766dfa0b62336ed9ca201bcc098cc612d6ac457628106e183b75'
	'4d2de1df11dccb4f1022c29f4dd9062c08869f7008e9e11135b5814dd035bbee')

prepare() {
	mkdir -p "$pkgname-$pkgver"
	bsdtar -xC "$pkgname-$pkgver" -f data.tar.xz
	cd "$pkgname-$pkgver"
}

package() {
	cd "$pkgname-$pkgver"
	cp -R etc "${pkgdir}/etc"
	cp -R usr "${pkgdir}/usr"
	rsync -av --exclude forticlient/gui/ opt/ "${pkgdir}/opt"
	install -Dm 0644 opt/forticlient/gui/FortiClient-linux-x64/resources/app.asar "$pkgdir"/opt/forticlient/gui/FortiClient-linux-x64/resources/app.asar
	cp -R lib "${pkgdir}/usr/lib"
	cp -R var "${pkgdir}/var"

	install -Dm 0755 "$srcdir"/FortiClient "$pkgdir"/opt/forticlient/gui/FortiClient-linux-x64/FortiClient
}
