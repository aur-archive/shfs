# $Id: PKGBUILD 82 2009-07-17 19:56:55Z aaron $
# Contributor: Jaroslaw Swierczynski <swiergot@juvepoland.com>

pkgname=shfs
pkgver=0.35
_kernver=2.6.22-ARCH
pkgrel=13
pkgdesc="SHell FileSystem Linux kernel module"
arch=('i686' 'x86_64')
url="http://shfs.sourceforge.net/"
license=('GPL2')
depends=('kernel26' 'shfs-utils')
install=$pkgname.install
source=(http://downloads.sourceforge.net/sourceforge/shfs/$pkgname-$pkgver.tar.gz \
	http://atrey.karlin.mff.cuni.cz/~qiq/src/shfs/shfs-$pkgver/space_chars.diff \
	http://atrey.karlin.mff.cuni.cz/~qiq/src/shfs/shfs-$pkgver/uidgid32.diff \
	http://atrey.karlin.mff.cuni.cz/~qiq/src/shfs/shfs-$pkgver/df.diff \
	http://atrey.karlin.mff.cuni.cz/~qiq/src/shfs/shfs-$pkgver/gcc4-compilefix.patch \
	http://atrey.karlin.mff.cuni.cz/~qiq/src/shfs/shfs-$pkgver/d_entry-2.6.16.diff \
	inode-bugfix.diff 2618fix.diff shfs-inode-and-fs.patch)
md5sums=('016f49d71bc32eee2b5d11fc1600cfbe' 'e5f37f793e95acdfd8e89affe9949160'\
         '29e5b080a1744f8283b8f55d5b904a60' '29b3f063e5feb8c259abc86d07f92f85'\
         '2b21af8aeef7fd2410e48dad73cb2633' '23d4ad14fd92a038647d1f21b7abac18'\
         '1f46232b6531f0ce990f091dfdeea3e4' 'd3d022b4dfb3f6cab5ac8fca8552091f'\
         'ce9993ac4e4881959578501fbfc33691')

build() {
  cd $startdir/src/$pkgname-$pkgver

  patch -Np0 -i ../space_chars.diff || return 1
  patch -Np0 -i ../uidgid32.diff || return 1
  patch -Np0 -i ../df.diff || return 1
  patch -Np1 -i ../gcc4-compilefix.patch || return 1
  patch -Np0 -i ../d_entry-2.6.16.diff || return 1
  patch -Np1 -i ../inode-bugfix.diff || return 1
  patch -Np1 -i ../2618fix.diff || return 1
  patch -Np0 -i ../shfs-inode-and-fs.patch || return 1

  sed -i "s!^KERNEL=.*\$!KERNEL=${_kernver}!" Makefile

  make module || return 1
  make ROOT=$startdir/pkg module-install

  sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/*.install
}
