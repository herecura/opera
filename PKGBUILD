# vim:set ft=sh:
# Maintainer: BlackEagle < ike DOT devolder AT gmail DOT com >
# Contributor: Bartłomiej Piotrowski <barthalion@gmail.com>
# Contributor: Mateusz Herych <heniekk@gmail.com>
# Contributor: ruario <ruario AT opera DOT com>
# Contributor: Daniel Isenmann <daniel AT archlinux DOT org>
# Contributor: dorphell <dorphell AT archlinux DOT org>
# Contributor: Sigitas Mazaliauskas <sigis AT gmail DOT com>
# Contributor: eworm

pkgname=opera
pkgver=66.0.3515.36
pkgrel=1
pkgdesc="A fast and secure web browser"
url="https://www.opera.com/"
options=(!strip !zipman)
license=('custom:opera')
backup=("etc/$pkgname/default")
arch=('x86_64')
depends=('gtk3' 'alsa-lib' 'libnotify' 'curl' 'nss' 'libcups' 'libxss' 'ttf-font' 'desktop-file-utils' 'shared-mime-info' 'hicolor-icon-theme')
optdepends=(
    'opera-ffmpeg-codecs: playback of proprietary video/audio'
    'pepper-flash: flash support'
    'upower: opera battery save'
)
source=(
    "https://get.geo.opera.com/pub/${pkgname}/desktop/${pkgver}/linux/${pkgname}-stable_${pkgver}_amd64.deb"
    "opera"
    "default"
    'eula.html'
    'terms.html'
    'privacy.html'
)
sha512sums=('fd600bacd367b1ffecb4b9425c7f7a61433df661dabbb34bed1b3c7e489c4ffe8bac7f74c160a61feb19b5ada6006baf58a67e6bbf156880e05cf6fe5e274ed8'
            '7e854e4c972785b8941f60117fbe4b88baeb8d7ca845ef2e10e8064043411da73821ba1ab0068df61e902f242a3ce355b51ffa9eab5397ff3ae3b5defd1be496'
            'ddb1773877fcfd7d9674e63263a80f9dd5a3ba414cda4cc6c411c88d49c1d5175eede66d9362558ddd53c928c723101e4e110479ae88b8aec4d2366ec179297f'
            '3606926b7a9dc281654a4478b0b43106c80e971b3e4548e313a7e31b56a08d248f552109007b549808bc1b80d51fb9fff8a99b42d6d618e2821779176f3337e2'
            '49c88283c2b289bcf967a4529c2d1646abd30973277ccee973745f8a014120bb152c7ff81eb9a72b7364249aef272da594154ab15eb64f2078e6af4be9df85db'
            'd314668fbd827c93cadb84a2d3953b7e58602defd1e6be1abfefa2557188bada4d4b49645bea1173ed6c47a4aaa1125d4d04ab2169b8a8d2eeff01545fa77999')

prepare() {
    sed -e "s/%pkgname%/$pkgname/g" -i "$srcdir/opera"
    sed -e "s/%operabin%/$pkgname\/$pkgname/g" \
        -i "$srcdir/opera"

}

package() {
    tar -xf data.tar.xz --exclude=usr/share/{lintian,menu} -C "$pkgdir/"

    # get rid of the extra subfolder {i386,x86_64}-linux-gnu
    (
        cd "$pkgdir/usr/lib/"*-linux-gnu/
        mv "$pkgname" ../
    )
    rm -rf "$pkgdir/usr/lib/"*-linux-gnu

    # suid opera_sandbox
    chmod 4755 "$pkgdir/usr/lib/$pkgname/opera_sandbox"

    # install default options
    install -Dm644 "$srcdir/default" "$pkgdir/etc/$pkgname/default"

    # install opera wrapper
    rm "$pkgdir/usr/bin/$pkgname"
    install -Dm755 "$srcdir/opera" "$pkgdir/usr/bin/$pkgname"

    # license
    install -Dm644 \
        "$pkgdir/usr/share/doc/${pkgname}-stable/copyright" \
        "$pkgdir/usr/share/licenses/$pkgname/copyright"

    # eula
    install -Dm644 \
        "$srcdir/eula.html" \
        "$pkgdir/usr/share/licenses/$pkgname/eula.html"

    # terms
    install -Dm644 \
        "$srcdir/terms.html" \
        "$pkgdir/usr/share/licenses/$pkgname/terms.html"

    # privacy
    install -Dm644 \
        "$srcdir/privacy.html" \
        "$pkgdir/usr/share/licenses/$pkgname/privacy.html"
}

