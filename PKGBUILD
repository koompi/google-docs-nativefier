# Maintainer: IsaacJreay <Isaac Jackson Reay at gmail dot com>

pkgname=google-docs-nativefier
pkgver=2
pkgrel=1
pkgdesc="Electron wrapper for the Google Docs web application"
arch=(x86_64)
license=(MIT)
url=https://docs.google.com
source=($pkgname.png
        $pkgname.desktop)
depends=("nodejs" "npm" "unzip")
sha256sums=('5231652761dce688ddd2f4b2a5b958fd5486acaa181ec239fd9d330d835b5bbb'
            'e3f241fc5eba29bf3f5f4ade5fb7cf4ca9426a1ddc34548d7224e5b372db49e4')

_instname=GoogleDocs


prepare(){
	cd "${srcdir}"
	npm i -g nativefier
}

build() {
    nativefier "https://docs.google.com/" \
      --icon $pkgname.png \
      --maximize \
      --name "$_instname" \
      --user-agent "Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.7113.93 Safari/537.36" \
      --internal-urls "(.*?docs\.google\.com.*?|.*?accounts\.google\.com.*?)" \
      --single-instance 
}

package() {
    install -d "$pkgdir"/opt "$pkgdir"/usr/{bin,share/pixmaps}
    install -Dm644 $pkgname.desktop "$pkgdir"/usr/share/applications/$_instname.desktop

    cp -rL $_instname-linux-* "$pkgdir"/opt/$pkgname
    ln -sf /opt/$pkgname/$_instname "$pkgdir"/usr/bin/$_instname
    ln -sf /opt/$pkgname/resources/app/icon.png "$pkgdir"/usr/share/pixmaps/$_instname.png

    chmod 666 "$pkgdir"/opt/$pkgname/resources/app/nativefier.json
}
