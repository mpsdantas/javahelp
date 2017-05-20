# Solution for javahelp2 2.0.05.r89-1.
### [Creator of the repository in the AUR of the arch and its information](https://aur.archlinux.org/packages/javahelp2/)

Recently, oracle moved the link from the "javahelp2" repository to some "strange" location and some archlinux users are having problems installing scilab, as scilab relies on "javahelp2".

## Solution

You can usually proceed with the installation of scilab or javahelp2.

```bash
yaourt -S scilab

yaourt javahelp2
```
When prompted for an edit of PKGBUILD enter an option 'y':

You should change the source and remove the pkver so that your PKGBUILD looks like this:

```bash
# Maintainer: Victor Dmitriyev <mrvvitek@gmail.com>
# Contributor: eolianoe <eolianoe [at] gmail [DoT] com>
# Contributor: Alucryd <alucryd at gmail dot com>
# Contributor: Stefan Husmann <stefan-husmann at t-online dot de>
# Contributor: Simon Lipp <sloonz+aur at gmail dot com>

pkgname=javahelp2
pkgver=2.0.05.r89
pkgrel=1
pkgdesc="Java based help system"
arch=('any')
url="https://javahelp.java.net/"
#"https://java.net/projects/javahelp/"
license=(GPL2)
makedepends=('apache-ant' 'subversion')
depends=('java-runtime')
source=("https://codeload.github.com/mpsdantas/javahelp/zip/master")
sha256sums=('SKIP')


build(){
    cd "${srcdir}/${pkgname}/trunk/javahelp_nbproject"
    ant release
}

package() {
    cd "${srcdir}/${pkgname}/trunk/javahelp_nbproject/dist/lib"
    install -dm755 "${pkgdir}/usr/share/java/javahelp"
    install -m644 -- *.jar "${pkgdir}/usr/share/java/javahelp"
    cd ../bin
    install -m644 -- *.jar "${pkgdir}/usr/share/java/javahelp"
    cd ../../lib
    # These are jars from tomcat5 and jdic-stub.jar
    install -m644 -- *.jar "${pkgdir}/usr/share/java/javahelp"
}
```

Once this is done the repository will be cloned, still to a problem that I solved in a "grotesque" way for now, execute those codes that the folder will be found:


```bash
cd /tmp/yaourt-tmp-youruser/aur-javahelp2/src/
mv javahelp-master/ javahelp2
```

Finally restart your compilation and the problem will be solved :)

Any questions or suggestions contact us by e-mail: mpsdantas15@gmail.com
