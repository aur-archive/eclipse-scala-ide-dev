#Maintainer: Andrzej Giniewicz <gginiu@gmail.com>
#Contributor: Kristof Jozsa <kjozsa@fsdev.hu>

pkgname=eclipse-scala-ide-dev
pkgver=4.0.0_RC2
pkgrel=1
pkgdesc="Scala IDE for Eclipse, development version"
arch=('any')
url="http://www.scala-ide.org/"
license=('custom')
depends=('eclipse>=4.4')
provides=('eclipse-scala-ide')
conflicts=('eclipse-scala-ide')

source=($pkgname-$pkgver.zip::"http://download.scala-ide.org/sdk/lithium/e44/scala211/dev/update-site.zip"
	"LICENSE" "scala-ide.desktop" "product.png"
)
md5sums=('55c5770f97cf2ae5d85a6da43b1cb3a2'
         '58b225f304aaf42c8b8738894a10cb96'
         '205ac79eeebb9cc43f9a0c836e60cf82'
         'c95b1920928f10d2c982afd7f5827a2c')

package() {
  install -D -m0644 "$srcdir"/LICENSE "$pkgdir"/usr/share/licenses/${pkgname}/LICENSE
  install -D -m0644 "$srcdir"/scala-ide.desktop "$pkgdir"/usr/share/applications/scala-ide.desktop
  install -D -m0644 "$srcdir"/product.png "$pkgdir"/usr/share/eclipse/dropins/scala-ide/icon.png

  _dest="${pkgdir}"/usr/share/eclipse/dropins/${pkgname/eclipse-}/eclipse
  cd "${srcdir}"/site

  # Features
  find features -type f | while read _feature ; do
    if [[ ${_feature} =~ (.*\.jar$) ]] ; then
      install -dm755 ${_dest}/${_feature%*.jar}
      cd ${_dest}/${_feature/.jar}
      jar xf ${srcdir}/site/${_feature}
    else
      install -Dm644 ${_feature} "${_dest}"/${_feature}
    fi
  done

  # Plugins
  find plugins -type f | while read _plugin ; do
    install -Dm644 ${_plugin} "${_dest}"/${_plugin}
  done
}
