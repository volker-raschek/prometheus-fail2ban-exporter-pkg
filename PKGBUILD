# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=prometheus-fail2ban-exporter
_pkgname=fail2ban-prometheus-exporter
pkgver=0.7.2
pkgrel=3
pkgdesc="Fail2Ban exporter for Fail2Ban metrics"
arch=('x86_64')
url="https://gitlab.com/hectorjsmith/$_pkgname"
license=('MIT')
makedepends=('go')
optdepends=('fail2ban: for monitoring a local fail2ban daemon')
source=(
  "$url/-/archive/$pkgver/$_pkgname-$pkgver.tar.gz"
  'prometheus-fail2ban-exporter'
  'systemd.service'
  'sysusers.conf'
)
sha512sums=('b7691cc31c747965b8ac9e8f818d4411b716888be5c84c51bbe5e206022bf9b60f95abddc37c8011a412a40ba0665107e957a55b3acba5018fd5be85c442380e'
            '7f0a0770ac6f42a7bc0d6e38559da833b7cbc18f97c516418d596878537c12b5778e2705a451e16f3067ceb87ce60af2a705867b0962f7abd1a595a23902a3ba'
            '7918ea56dc94b29e25900d5bcf94c8c525226d5a490124b718686aa3c8900752baae80722c8c840d563c1ffef06a54440802cff498c9edf0c673d682518a3f1a'
            'c070f57c58f367421835fe757b6b46e4c6cc3a69e0e927b10c229daab945fc52e57acdf25a84f04f752cb7304c40c2ff95e7987daf41c80f8857d409def1752f')
b2sums=('87ab07b334594ecb792d817abb9bca1c7565be64df79d6dfa5edd268241534345a9e7e5b782dfcfd623d6a63db77b8803c614e44c3d44f9b7ca6b41952c6eb20'
        'cd565b9262d85399ba63290d5af32fed23227d4a987499968654d4f0f7ea95c91c7781cae513d4368a87de328ac198a5e05cf5beae9199ebbdfb622c098281b9'
        'e88ba4beef23dfd36a825f6b873647708b81a35d4b2debb16f0a5e35e5e42311ebd9694cb90501d65231c1ae45c863103fe93ae1f6c99c2745ed7e8c12434653'
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
