# Maintainer: Jed Brown <jedbrown>
pkgname=ptscotch-openmpi
pkgver=6.0.0
_pkgver=${pkgver}_esmumps
_downloadnum=31832              # gforge is insane
pkgrel=3
_prefix=/usr
pkgdesc="SCOTCH is a software package and libraries for graph, mesh and hypergraph partitioning, static mapping, and sparse matrix block ordering. This is the Parallel version using MPI."
url="http://www.labri.fr/perso/pelegrin/scotch/"
license="custom: CeCILL-C"
depends=('openmpi')
provides=()
conflicts=()
replaces=()
backup=()
options=(staticlibs)
arch=('i686' 'x86_64')
source=("http://gforge.inria.fr/frs/download.php/${_downloadnum}/scotch_${_pkgver}.tar.gz")
md5sums=('c50d6187462ba801f9a82133ee666e8e')

build() {
  cd "${srcdir}/scotch_${_pkgver}"

  cd src
  sed "s,-O3,$CFLAGS -fPIC,g" Make.inc/Makefile.inc.x86-64_pc_linux2 > Makefile.inc
  sed -i "s,= mpicc,= ${_prefix}/bin/mpicc,g" Makefile.inc
  sed -i "/CCD/ c CCD\t\t= ${_prefix}/bin/mpicc" Makefile.inc

  make ptscotch
}

package() {
  cd "${srcdir}/scotch_${_pkgver}"
  install -d "${pkgdir}/${_prefix}"/{bin,lib,include/scotch}
  install -m 644 -t "${pkgdir}/${_prefix}"/include/scotch include/*.h
  install -m 644 -t "${pkgdir}/${_prefix}"/lib lib/lib*.a
  install -m 755 -t "${pkgdir}/${_prefix}"/bin bin/*
  install -m 644 -D "${srcdir}/scotch_${_pkgver}/doc/CeCILL-C_V1-en.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
