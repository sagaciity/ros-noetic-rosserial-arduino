pkgdesc="ROS - rosserial for Arduino/AVR platforms."
url='https://wiki.ros.org/rosserial_arduino'

pkgname='ros-noetic-rosserial-arduino'
pkgver='0.9.2'
arch=('any')
pkgrel=2
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
    	ros-noetic-message-generation
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-rospy
    ros-noetic-rosserial-msgs
    ros-noetic-message-runtime
    ros-noetic-rosserial-python
)

depends=(
    	arduino-avr-core
	${ros_depends[@]}
)

_dir="rosserial-${pkgver}/rosserial_arduino"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-drivers/rosserial/archive/${pkgver}.tar.gz")
sha256sums=('10544be94241499aa3b019aea6d7cb40546ea484749e909cee31a928c7d40465')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Fix Python2/Python3 conflicts.

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python3 \
		-DPYTHON_INCLUDE_DIR=/usr/include/python3.7m \
		-DPYTHON_LIBRARY=/usr/lib/libpython3.7m.so \
		-DPYTHON_BASENAME=.cpython-37m \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
