pkgname=nginx-mod-http-flv
pkgver=442.9218647
pkgrel=1

_modname="nginx-http-flv-module"
_nginxver="$(/bin/nginx -v 2>&1 | grep -Eo '([[:digit:]]|\.)+')"

pkgdesc='About Media streaming server based on nginx-rtmp-module. In addtion to the features nginx-rtmp-module provides, HTTP-FLV, GOP cache and VHOST (one IP for multi domain names) are supported now.'
arch=('i686' 'x86_64')
depends=('nginx' 'openssl')
provides=("$_modname")
url='https://github.com/winshining/nginx-http-flv-module'
license=('BSD')

source=(
        "http://nginx.org/download/nginx-$_nginxver.tar.gz"
        "$_modname::git+https://github.com/winshining/nginx-http-flv-module.git"
)
sha256sums=(
        'SKIP'
        'SKIP'
)

pkgver() {
        cd "$_modname"
        printf "%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
        cd "nginx-$_nginxver"
        ./configure --with-compat "--add-dynamic-module=../$_modname"
        make modules
}

package() {
        cd "$_modname"
        install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
        cd "../nginx-$_nginxver/objs"
        install -Dm755 ngx_http_flv_live_module.so "$pkgdir/usr/lib/nginx/modules/ngx_http_flv_live_module.so"
}
