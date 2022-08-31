pkgname=krita-patched
_pkgname=krita
_pkgver=5.1.0
pkgver=${_pkgver/-/}
pkgrel=1
pkgdesc='Krita (painting software) with a patch for a focus-switch bug (428080)'
arch=(x86_64)
provides=(krita)
conflicts=(krita)
url='https://krita.org'
license=(GPL3)
depends=(kitemviews kitemmodels ki18n kcompletion kguiaddons kcrash qt5-svg qt5-multimedia quazip
         gsl libraw exiv2 openexr fftw openjpeg2 opencolorio libwebp hicolor-icon-theme)
makedepends=(extra-cmake-modules kdoctools boost eigen poppler-qt5 python-pyqt5 libheif
             qt5-tools sip kseexpr libmypaint libjxl xsimd)
optdepends=('poppler-qt5: PDF filter' 'ffmpeg: to save animations'
            'python-pyqt5: for the Python plugins' 'libheif: HEIF filter'
            'kseexpr: SeExpr generator layer' 'kimageformats: PSD support' 'libmypaint: support for MyPaint brushes'
            'krita-plugin-gmic: GMic plugin') # 'libjxl: JPEG-XL filter'
source=(https://download.kde.org/stable/krita/$_pkgver/$_pkgname-$_pkgver.tar.gz{,.sig}
        key-focus.patch)
sha256sums=('9a3b3f5858480b7091bd48449926e613538ea8a4dc06249c860ffe3da5acd882'
            'SKIP'
            'SKIP')
validpgpkeys=('05D00A8B73A686789E0A156858B9596C722EA3BD'  # Boudewijn Rempt <foundation@krita.org>
              'E9FB29E74ADEACC5E3035B8AB69EB4CF7468332F'  # Dmitry Kazakov (main key) <dimula73@gmail.com>
              '064182440C674D9F8D0F6F8B4DA79EDA231C852B') # Stichting Krita Foundation <foundation@krita.org>
options=(debug)

prepare() {
  pushd "$srcdir/$_pkgname-$_pkgver"
  patch -Np1 -i "$srcdir/key-focus.patch"
  popd
}

build() {
  cmake -B build -S "$_pkgname-$_pkgver" \
    -DBUILD_KRITA_QT_DESIGNER_PLUGINS=ON
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
