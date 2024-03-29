pkgname=krita-patched
_pkgname=krita
_pkgver=5.1.5
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
            'krita-plugin-gmic: GMic plugin' 'libjxl: JPEG-XL filter')
source=(https://download.kde.org/stable/krita/$_pkgver/$_pkgname-$_pkgver.tar.gz{,.sig}
        find-xsimd.patch
        https://invent.kde.org/graphics/krita/-/commit/e9184281.patch
        https://invent.kde.org/graphics/krita/-/commit/bbee5eff.patch
        exiv2-0.28.patch
        key-focus.patch)
sha256sums=('1c775ebef0f799a9a6b74440c3d906ab913c27541b177ed621704de714e9a4d3'
            'SKIP'
            'SKIP'
            '3db041acee92d6e4238c47ad572142a930340858703f523baa32f129e6474060'
            '0f52ba825ce0432e55c1c673d8ebbd34f4353470a6c27bdc55beb2a5446f9a4a'
            'SKIP'
            'SKIP')
validpgpkeys=('05D00A8B73A686789E0A156858B9596C722EA3BD'  # Boudewijn Rempt <foundation@krita.org>
              'E9FB29E74ADEACC5E3035B8AB69EB4CF7468332F'  # Dmitry Kazakov (main key) <dimula73@gmail.com>
              '064182440C674D9F8D0F6F8B4DA79EDA231C852B') # Stichting Krita Foundation <foundation@krita.org>

prepare() {
  patch -d $_pkgname-$_pkgver -p1 < find-xsimd.patch
  patch -d $_pkgname-$_pkgver -p1 < e9184281.patch # Fix build with libheif 1.14.1
  patch -d $_pkgname-$_pkgver -p1 < bbee5eff.patch # Fix crash when loading some TIFF files
  patch -d $_pkgname-$_pkgver -p1 < exiv2-0.28.patch # Fix build with exiv2 0.28

  patch -d $_pkgname-$_pkgver -p1 < key-focus.patch
}

build() {
  cmake -B build -S $_pkgname-$_pkgver \
    -DBUILD_KRITA_QT_DESIGNER_PLUGINS=ON
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
