pkgdesc="ROS - rospy is a pure Python client library for ROS."
url='https://wiki.ros.org/rospy'

pkgname='ros-noetic-rospy'
pkgver='1.15.14'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(
    ros-noetic-catkin
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-genpy
    ros-noetic-rosgraph-msgs
    ros-noetic-std-msgs
    ros-noetic-roscpp
    ros-noetic-rosgraph
    ros-noetic-roslib
)

depends=(
    ${ros_depends[@]}
    python-yaml
    python-rospkg
    python-numpy
)

_dir="ros_comm-${pkgver}/clients/rospy"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros/ros_comm/archive/${pkgver}.tar.gz")
sha256sums=('1083b58470a81323bc3a13aa9ae7c813e9fbc27b18f0e95a76b53e4076f3d872')

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
