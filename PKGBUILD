# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-fail2ban-exporter
_pkgname=fail2ban-prometheus-exporter
pkgver=0.10.3 # renovate: datasource=gitlab-releases depName=hctrdev/fail2ban-prometheus-exporter
pkgrel=1
pkgdesc="Fail2Ban exporter for Fail2Ban metrics"
arch=('armv7h' 'aarch64' 'x86_64')
url="https://gitlab.com/hctrdev/$_pkgname"
license=('MIT')
makedepends=('go')
optdepends=('fail2ban: for monitoring a local fail2ban daemon')
source=(
  "$url/-/archive/v$pkgver/$_pkgname-v$pkgver.tar.gz"
  'prometheus-fail2ban-exporter'
  'systemd.service'
  'sysusers.conf'
)

sha512sums=('1258f917430815c82661a25ad17dc428b989e4a312c4fc313e80982d5ddf98014765de8ca2cff4db9811adb2dbfc99c70a22393330ea0c672a6fe5865106c7a0'
            '681a744d7a7d7825d857b5d14ea19fefe0302de2d98fa76a2442335ecc7cf4cf2dfd03aa8fe9b3356544ef29b0823279a3810c78eabbf8be6c88a0a71f509967'
            'f9f85bdd72d6f8bcb17732bb954c2ff0c19dfcfcdce6751713f0905f6405eb34cf211b974311217ca60dabb6fa274ec26799f43432c2ad63284a2894dda12092'
            'c070f57c58f367421835fe757b6b46e4c6cc3a69e0e927b10c229daab945fc52e57acdf25a84f04f752cb7304c40c2ff95e7987daf41c80f8857d409def1752f')
b2sums=('4156605955d2345520b2ffc5ef39c749b0fad350fa5c8cbf3139817335ed1c1d165fa97ffbdf4a2e31609f93140c716b84b824f382618c3c58e35f94098d5e58'
        '3d6adfad59d88ff99b1e4f924651746e62e562fefa0360f02fe1091e920b0bb74e4f54930ff1f863b9004a490e90c78dc92d16ca234b5b536315b7fd45cbf4e4'
        '0334daf62d9980a8165f8701041af27889e5501cba3d5790fdae03a812d6fd3a48b6d9dcf67bd25fb56ac762d9332f27c7e4ea08c56b0f5e657268caf7018ee8'
        '4b731a290e1ad967f9e7708b00d4b9279bdbc57461c62d09a8bff00958e72cb8e69848d73af486bcc9e58ffe1e087ca86dc2625770a25ebd47e41d7bba193bef')

build() {
  cd "$_pkgname-$pkgver/src"
  go build -v \
    -buildmode=pie \
    -trimpath \
    -o $pkgname .
}

package() {
  # systemd integration
  install -D --mode 0644 systemd.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
  install -D --mode 0644 sysusers.conf "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"

  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$_pkgname-$pkgver/src/$pkgname"

  # extra args
  # NOTE: Set restrict file permissions by default to protect optional basic auth credentials
  install -D --mode 0600 --target-directory "$pkgdir/etc/conf.d" prometheus-fail2ban-exporter

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$_pkgname-$pkgver/LICENSE"
}
