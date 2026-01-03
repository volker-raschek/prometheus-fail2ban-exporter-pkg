# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-fail2ban-exporter
_pkgname=fail2ban-prometheus-exporter
pkgver=0.10.3 # renovate: datasource=gitlab-releases depName=hctrdev/fail2ban-prometheus-exporter
_pkgver=v${pkgver}
pkgrel=1
pkgdesc="Fail2Ban exporter for Fail2Ban metrics"
arch=('armv7h' 'aarch64' 'x86_64')
url="https://gitlab.com/hctrdev/$_pkgname"
license=('MIT')
makedepends=('go')
optdepends=('fail2ban: for monitoring a local fail2ban daemon')
source=(
  "$url/-/archive/$_pkgver/$_pkgname-$_pkgver.tar.gz"
  'prometheus-fail2ban-exporter'
  'systemd.service'
)

sha512sums=('1258f917430815c82661a25ad17dc428b989e4a312c4fc313e80982d5ddf98014765de8ca2cff4db9811adb2dbfc99c70a22393330ea0c672a6fe5865106c7a0'
            '681a744d7a7d7825d857b5d14ea19fefe0302de2d98fa76a2442335ecc7cf4cf2dfd03aa8fe9b3356544ef29b0823279a3810c78eabbf8be6c88a0a71f509967'
            'f9f85bdd72d6f8bcb17732bb954c2ff0c19dfcfcdce6751713f0905f6405eb34cf211b974311217ca60dabb6fa274ec26799f43432c2ad63284a2894dda12092')
b2sums=('4156605955d2345520b2ffc5ef39c749b0fad350fa5c8cbf3139817335ed1c1d165fa97ffbdf4a2e31609f93140c716b84b824f382618c3c58e35f94098d5e58'
        '3d6adfad59d88ff99b1e4f924651746e62e562fefa0360f02fe1091e920b0bb74e4f54930ff1f863b9004a490e90c78dc92d16ca234b5b536315b7fd45cbf4e4'
        '0334daf62d9980a8165f8701041af27889e5501cba3d5790fdae03a812d6fd3a48b6d9dcf67bd25fb56ac762d9332f27c7e4ea08c56b0f5e657268caf7018ee8')

build() {
  cd "$_pkgname-$_pkgver"
  go build -v \
    -buildmode=pie \
    -trimpath \
    -o $pkgname .
}

package() {
  # systemd integration
  install -D --mode 0644 systemd.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"

  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$_pkgname-$_pkgver/$pkgname"

  # extra args
  # NOTE: Set restrict file permissions by default to protect optional basic auth credentials
  install -D --mode 0600 --target-directory "$pkgdir/etc/conf.d" "$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$_pkgname-$_pkgver/LICENSE"
}
