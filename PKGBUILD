
pkgdesc="ROS - This package is a ROS wrapper for Alvar, an open source AR tag tracking library."
url='http://www.ros.org/'

pkgname='ros-hydro-ar-track-alvar'
pkgver='0.4.1'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-message-generation
  ros-hydro-tf2
  ros-hydro-cv-bridge
  ros-hydro-resource-retriever
  ros-hydro-rospy
  ros-hydro-sensor-msgs
  ros-hydro-image-transport
  ros-hydro-roscpp
  ros-hydro-geometry-msgs
  ros-hydro-catkin
  ros-hydro-std-msgs
  ros-hydro-tf
  ros-hydro-visualization-msgs
  ros-hydro-dynamic-reconfigure
  ros-hydro-pcl-ros
  ros-hydro-pcl-conversions)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]}
  tinyxml)

ros_depends=(ros-hydro-tf2
  ros-hydro-cv-bridge
  ros-hydro-resource-retriever
  ros-hydro-rospy
  ros-hydro-message-runtime
  ros-hydro-sensor-msgs
  ros-hydro-image-transport
  ros-hydro-roscpp
  ros-hydro-geometry-msgs
  ros-hydro-std-msgs
  ros-hydro-tf
  ros-hydro-visualization-msgs
  ros-hydro-dynamic-reconfigure
  ros-hydro-pcl-ros
  ros-hydro-pcl-conversions)
depends=(${ros_depends[@]}
  tinyxml)

_tag=release/hydro/ar_track_alvar/${pkgver}-${_pkgver_patch}
_dir=ar_track_alvar
source=("${_dir}"::"git+https://github.com/ros-gbp/ar_track_alvar-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
