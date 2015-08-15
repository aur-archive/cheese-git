# Maintainer: alesko <askondro@gmail.com>

pkgname=cheese-git
pkgver=20140704
pkgrel=1
pkgdesc="Cheese uses your webcam to take photos and videos, applies fancy special effects and lets you share the fun with others"
arch=(i686 x86_64)
url="http://projects.gnome.org/cheese"
license=('LGPL')
depends=('gnome-desktop' 'gtk3' 'libcanberra' 'librsvg' 
           'clutter-gst' 'clutter-gtk' 'mx' 'libgee'
           'gnome-video-effects' 'hicolor-icon-theme' 'dconf' 'cogl' 'gst-plugins-bad')
makedepends=('pkgconfig' 'gnome-doc-utils' 'intltool' 'gobject-introspection'
'itstool' 'nautilus-sendto' 'vala' 'gtk-doc' 'yelp-tools' 'gnome-common' 'appdata-tools' )
options=('!libtool' '!emptydirs')
provides=('cheese')
conflicts=('cheese' 'cheese-git')
install=cheese.install
source=()
md5sums=()

_gitroot="git://git.gnome.org/cheese"
_gitname="cheese"

build() {
  cd $srcdir
  msg "Connecting to git://git.gnome.org/cheese GIT server...."

  if [ -d $srcdir/$_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -Rf $srcdir/$_gitname-build
  git clone $srcdir/$_gitname $srcdir/$_gitname-build
  cd $srcdir/$_gitname-build

  msg "Starting build"
  ./autogen.sh
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
      --disable-static --disable-schemas-compile
  make

}

package() {
  cd $srcdir/$_gitname-build
  make DESTDIR=$pkgdir install
}
