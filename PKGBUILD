# Maintainer: josephgbr <rafael.f.f1 at gmail.com>

pkgname=dbdesigner
pkgver=4.0.5.4
pkgrel=1
pkgdesc="fabFORCE's visual database design system"
arch=(i686 x86_64)
url="http://www.fabforce.net/dbdesigner4/index.php"
license=('GPL')
if [ $CARCH == x86_64 ]; then
	depends=('lib32-kylixlibs' 'lib32-libmng' 'lib32-gcc-libs')
	_libdir=usr/lib32/DBDesigner4
else
	depends=('kylixlibs' 'libmng')
	_libdir=usr/lib/DBDesigner4
fi
source=(http://downloads.mysql.com/DBDesigner4/DBDesigner$pkgver.tar.gz
        dbdesigner.desktop
        dbdesigner)
md5sums=('3a9bfd9b40fb8b70e24fd2195424cb51'
         '9ad96f433c24981960066d8f11a819ac'
         'c228252e9f78cac64f232d1f07ffed4b')

package() {
  cd "$srcdir/DBDesigner4"  

  # install DBDesigner4 core files
  install -d "$pkgdir/opt/DBDesigner4"
  cp -af * "$pkgdir/opt/DBDesigner4"
  cd "$pkgdir/opt/DBDesigner4"
  
  # install binary, icon and desktop files
  install -Dm755 "$srcdir/dbdesigner" \
                 "$pkgdir/usr/bin/dbdesigner"
  install -Dm644 Gfx/Icon48.xpm \
                 "$pkgdir/usr/share/pixmaps/dbdesigner.xpm"
  install -Dm644 "$srcdir/dbdesigner.desktop" \
                 "$pkgdir/usr/share/applications/dbdesigner.desktop"
                
  
  # install library in "$_libdir" (/usr/lib/DBDesigner4 or /usr/lib32/DBDesigner4)
  for i in $(ls Linuxlib); do
  	install -Dm755 Linuxlib/$i "$pkgdir/$_libdir/$i"
  done
  ln -s bplrtl.so.6.9.0 "$pkgdir/$_libdir/bplrtl.so.6.9"
  ln -s dbxres.en.1.0 "$pkgdir/$_libdir/dbxres.en.1"
  ln -s libmidas.so.1.0 "$pkgdir/$_libdir/libmidas.so.1"
  ln -s libmysqlclient.so.10.0.0 "$pkgdir/$_libdir/libmysqlclient.so"
  ln -s libqt.so.2.3.2 "$pkgdir/$_libdir/libqt.so.2"
  ln -s libqtintf-6.9.0-qt2.3.so "$pkgdir/$_libdir/libqtintf-6.9-qt2.3.so"
  ln -s libsqlmy23.so.1.0 "$pkgdir/$_libdir/libsqlmy23.so"
  ln -s libsqlmy23.so "$pkgdir/$_libdir/libsqlmy.so"
  ln -s libsqlora.so.1.0 "$pkgdir/$_libdir/libsqlora.so"
  ln -s libDbxSQLite.so.2.8.5 "$pkgdir/$_libdir/libDbxSQLite.so"
  ln -s liblcms.so.1.0.9 "$pkgdir/$_libdir/liblcms.so"
  ln -s libpng.so.2.1.0.12 "$pkgdir/$_libdir/libpng.so.2"
  ln -s libstdc++.so.5.0.0 "$pkgdir/$_libdir/libstdc++.so.5"
  
  # package cleanup
  rm DBDesigner4.spec   # RPM pkgs related (not Archlinux)
  rm startdbd.desktop   # Replaced by dbdesigner.desktop
  rm startdbd           # Replaced by dbdesigner
  rm -rf Linuxlib	# Redundant: already in $_libdir
  rm "$pkgdir/$_libdir/deleteSymbolicLinks.sh"
}
