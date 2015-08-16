# Maintainer: Mitchell Johnson <mjjohnso@mtu.edu>
pkgname=mrpt-svn
pkgver=2831
pkgrel=2
pkgdesc="Provides an extensive set of libraries, algorithms, and applications employed in a number of mobile robotics research areas."
arch=('i686' 'x86_64')
url="http://www.mrpt.org"
license=('GPL3')
depends=('opencv' 'wxgtk' 'desktop-file-utils')
makedepends=('subversion' 'cmake')
optdepends=('ffmpeg: Video Support' 'freeglut' 'zlib'
            'libftdi' 'libdc1394' 'libusb: Kinect support'
            'pcl')
install=mrpt-svn.install
#md5sums=() #generate with 'makepkg -g'

_svntrunk=http://mrpt.googlecode.com/svn/trunk
_svnmod=$pkgname-$pkgver

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  mkdir "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_CXX_FLAGS="-fpermissive" \
    -DMRPT_OPTIMIZE_NATIVE=ON $srcdir/$_svnmod
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
