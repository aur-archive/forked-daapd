# Maintainer: Alexander Simonov <alex@simonov.me>
# Contributor: Kosta Welke <kosta@fillibach.de>
pkgname=forked-daapd
pkgver=23.1
pkgrel=1
pkgdesc="iTunes-compatible media server, originally intended as a rewrite of Firefly Media Server (mt-daapd)."
arch=('i686' 'x86_64')
url="https://github.com/ejurgensen/forked-daapd"
license=('GPL')
groups=()
depends=(pkg-config avahi sqlite3 ffmpeg confuse libevent mxml libgcrypt zlib libunistring flac taglib libplist libantlr3c libavl-for-forked-daapd)
makedepends=(gperf java-runtime)
optdepends=()
provides=()
conflicts=()
replaces=()
backup=(etc/forked-daapd.conf etc/avahi/services/forked-daapd.service)
options=()
install=forked-daapd.install
changelog=
source=(https://github.com/ejurgensen/forked-daapd/archive/$pkgver.tar.gz forked-daapd.install forked-daapd.avahi forked-daapd.service http://www.antlr3.org/download/antlr-3.4-complete.jar)
noextract=()
md5sums=('c2f791ff39d7c339c370f716202e0986'
         'bad1372140c914d1c312a186087fe375'
         'c01fde6f40880fed6092c0830a5f232e'
         '5047515b396f37a9030a003f12eaaafa'
         '1b91dea1c7d480b3223f7c8a9aa0e172')
sha1sums=('18775582c0cdb077f452cfc55657d6336e585121'
          '90a796470231ae7c22635c3fbbb47f9d8a61ebd6'
          'a6f3c5ee05365481caaa569fe15ca34ffe4dc847'
          '76623036d11d411cb438f9ac8f9cdf21f12b305f'
          '5cab59d859caa6598e28131d30dd2e89806db57f')
sha256sums=('e8b3220553b4e864b3cb2a4a947ced34263042c37c6cc18ea42878fae58d29a3'
            '19b394a38ac88247d6b7d939e648ac53e8f08bef852e76c79355d1231bffad3d'
            '0efc8aac56d2b3a70d74c90a72595f3b685a30ee94a278880cd0cc4db35fa113'
            'f623bfe983e65bd5c658bb456b775c62812e3daf8a5f27d154cf70c48c1e51bf'
            '9d3e866b610460664522520f73b81777b5626fb0a282a5952b9800b751550bf7')
sha384sums=('0cb40f0db16ca22bcfa49d05c0aee2acf6e680cdee7337b592dec5a81602cc027ebd91ff5062a5187e09292f1451954b'
            'b536551061e8404f0128e9313411c9f2419d7bf4c982c8d9f32300727c873219d90c90bda32256fb9d3bd560c0be2704'
            '36bdb6cfc389572f7f34658307b68f31d79ba9a5827eeee60c43f042f3d75d90c9d76e90840258e57e59c5c4d8d47d52'
            'a4dc8c4a504496a624e210ac668e5190eb6756a4f7f2825c42624f424723ddfd0c0338fa753ad1d61944d3bdf08451a7'
            'a2fbecb5fae6af12adcfb3801624d4941e25e4b526794f7b9a713ae8b6873962ca36a74f9220d7e0057aaa89d5ca6d68')
sha512sums=('6cc9869e4d196ee2cff2567ef6bf72f08c6717c27a1e43056180aafb11af176fce3f64329f5b255aa77fa1ea34e998a0628ca42b0dc73733bd6dd5724edf2b93'
            'f82c8b73b39e6b8e83b09953d187b98b9fb856914a0a231b6758701f4f383b5dd5368ec468011b78402fd9850662b61b48e6198336ed4049cfd1ed7cb8659e9b'
            '70da9a199ac821736ea6cd33455c14cf32ab5bc4b401dc31179dc6029c36fcb543810d0041f309fdcfd7be84d7d1f921b63a70993ad89b6f0c1ea06e51859dfb'
            'bc32f4cb705bf3890e85a51530818a1d86b260c1f6c1203b0f07757a8ab23b7654a357bc9c7ab10b370f4714f26b60368c1910c7efe9197041015183518a40d6'
            '04be4dfba3a21f3ab9d9e439a64958bd8e844a9f151b798383bd9e0dd6ebc416783ae7cb1d1dbb27fb7288ab9756b13b8338cdb8ceb41a10949c852ad45ab1f2')

build() {
  OLD_PATH=$PATH
  export PATH="$srcdir:$PATH"
  echo "#!/bin/bash" > antlr3
  echo "exec java -cp $srcdir/antlr-3.4-complete.jar org.antlr.Tool \"\$@\"" >> antlr3
  chmod a+x ./antlr3
  cd "$srcdir/$pkgname-$pkgver"
  echo $PATH
  autoreconf -i
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-flac --enable-musepack --enable-itunes --sbindir=/usr/bin
  make
  export PATH=$OLD_PATH
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  install -D -m644 $srcdir/forked-daapd.service $pkgdir/usr/lib/systemd/system/forked-daapd.service
  install -D -m644 $srcdir/forked-daapd.avahi $pkgdir/etc/avahi/services/forked-daapd.service
  make DESTDIR="$pkgdir/" install
}
