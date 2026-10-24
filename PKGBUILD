pkgname=deepseek-harness-tauri-bin
pkgver=0.25.0
pkgrel=1
pkgdesc='Native Tauri desktop application for DeepSeek Harness'
arch=('x86_64')
url='https://github.com/dsh-tauri/deepseek-harness-desktop'
license=('MIT')

depends=(
  'gst-plugins-good'
  'gst-plugins-bad'
  'libappindicator'
  'webkit2gtk-4.1'
  'gtk3'
  'python'
  'python-yaml'
)

optdepends=(
  'nodejs: required by some bundled extension/tool scripts'
)
provides=('deepseek-harness-desktop' 'dsh-tauri')
conflicts=('deepseek-harness-desktop' 'dsh-tauri')

source_x86_64=(
  "${pkgname}-${pkgver}.deb::https://github.com/dsh-tauri/deepseek-harness-desktop/releases/download/v${pkgver}/Deepseek.Harness.Desktop_${pkgver}_amd64.deb"
)

sha256sums_x86_64=('3c74478fc95fbfcc892d661df8572864a4ebe1806e95fee5bca0be943314a85b')

package() {
  cd "$srcdir"

  bsdtar -xf "${pkgname}-${pkgver}.deb"
  bsdtar -xf data.tar.* -C "$pkgdir"

  # Install icon into the standard icon theme path
  install -Dm644 \
    "$pkgdir/usr/lib/DSH Tauri/icons/32x32.png" \
    "$pkgdir/usr/share/icons/hicolor/32x32/apps/deepseek-harness-desktop.png"

  # Replace upstream desktop entry with a more searchable/freedesktop-friendly one
  install -Dm644 /dev/stdin \
    "$pkgdir/usr/share/applications/deepseek-harness-desktop.desktop" <<'EOF'
[Desktop Entry]
Type=Application
Name=DeepSeek Harness
GenericName=AI Agent Desktop
Comment=Desktop application for DeepSeek Harness
Exec=deepseek-harness-desktop %U
Icon=deepseek-harness-desktop
Terminal=false
StartupNotify=true
StartupWMClass=deepseek-harness-desktop
Categories=Development;Utility;
Keywords=DeepSeek;Harness;DSH;AI;Agent;
MimeType=x-scheme-handler/dsh;
EOF

  rm -f "$pkgdir/usr/share/applications/DSH Tauri.desktop"
}
