# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-fail2ban-exporter
_pkgname=fail2ban-prometheus-exporter
pkgver=0.7.2
pkgrel=2
pkgdesc="Fail2Ban exporter for Fail2Ban metrics"
arch=('x86_64')
url="https://gitlab.com/hectorjsmith/$_pkgname"
license=('MIT')
makedepends=('go')
optdepends=('fail2ban: for monitoring a local fail2ban daemon')
source=(
  "$url/-/archive/$pkgver/$_pkgname-$pkgver.tar.gz"
  'systemd.service'
  'sysusers.conf'
)
sha512sums=('b7691cc31c747965b8ac9e8f818d4411b716888be5c84c51bbe5e206022bf9b60f95abddc37c8011a412a40ba0665107e957a55b3acba5018fd5be85c442380e'
            '19a61f7a7be1c73cbe87a978f5787ae35304e2e6db03a927016e1a5a8b0715bc3d971e52da61ce5f1a7fd302ae7646a4c54c7fdc082ee9c371368d56be311d09'
            'c070f57c58f367421835fe757b6b46e4c6cc3a69e0e927b10c229daab945fc52e57acdf25a84f04f752cb7304c40c2ff95e7987daf41c80f8857d409def1752f')
b2sums=('87ab07b334594ecb792d817abb9bca1c7565be64df79d6dfa5edd268241534345a9e7e5b782dfcfd623d6a63db77b8803c614e44c3d44f9b7ca6b41952c6eb20'
        '126dae6e1a1fe9bcc67e2dafc203aeb5f057aea82fec65b4f8c18f5a4bc3154f9e22e53b043f9c6f849f625d4ecf77ea67be5bb562b0b794814ad695f48bd235'
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
  install -Dm644 systemd.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
  install -Dm644 sysusers.conf "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"

  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$_pkgname-$pkgver/src/$pkgname"
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$_pkgname-$pkgver/LICENSE"
}
