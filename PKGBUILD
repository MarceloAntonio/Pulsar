pkgname=orbit-bin
pkgver=latest
pkgrel=1
pkgdesc="A WiFi/Bluetooth manager for Wayland (Custom Fork)"
arch=('x86_64')
url="https://github.com/MarceloAntonio/wifi-bar"
license=('MIT')
depends=('gtk4' 'gtk4-layer-shell')
provides=('orbit')
conflicts=('orbit')

# O source normalmente baixa de um link estático com versão (ex: $pkgver). 
# Como as tags são geradas dinamicamente no GitHub Action, podemos apontar para o latest release
# usando uma URL de "latest" do GitHub.
source=("orbit::https://github.com/MarceloAntonio/wifi-bar/releases/latest/download/orbit")
sha256sums=('SKIP') # SKIP é usado aqui porque o binário 'latest' muda a cada novo commit.

package() {
    # Cria o diretório de destino se não existir
    install -d "${pkgdir}/usr/bin"
    
    # Instala o binário com permissão de execução
    install -m755 "${srcdir}/orbit" "${pkgdir}/usr/bin/orbit"
}
