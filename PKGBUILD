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
pkgver=68.0.3618.125
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
    "https://rpm.opera.com/rpm/opera_stable-$pkgver-linux-release-x64-signed.rpm"
    'eula.html'
    'terms.html'
    'privacy.html'
)
sha512sums=('12017d6764c7b4c4e2e1a5b317d30ecc3971fef809c8d7d6ee8fd67ca8ec457e14f75d084d171409ded930830fd75835bac146be9f497ceab0b6474c2bf64cce'
            'e181656876f5075988964187c3d9f8d68c62944b986d67927c1c6e3181aeebf63a71d416d913c96e2d35b19bf786d8c83ee10015924c278ba42c990bcb7f9bb5'
            '6076b2a32ba74dcd8df225a1a43932c923782453cd5653ef329f0b57f23d975a8d01af2eceefd72c70de990f22f01b651222294319dff871f816f1fa2967abf2'
            '3264c0a2e8a5c4f58fdc3de7bda99c954f5a74468ef2259778e2d21048c7e6e91847184a9fb846214b65d26c2737d6b49cf010276c94b6038e584324e4071eb5')

package() {
    install -dm755 "$pkgdir/usr/lib"
    cp -a usr/bin     "$pkgdir"/usr/
    cp -a usr/lib64/* "$pkgdir"/usr/lib/
    cp -a usr/share   "$pkgdir"/usr/

    # suid opera_sandbox
    chmod 4755 "$pkgdir/usr/lib/$pkgname/opera_sandbox"

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

