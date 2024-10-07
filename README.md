**FOLLOW U-VIP-SLAM FIRST**
installation deviations from U-VIP-SLAM (to be updated):

setup a WHOLE NEW build dir with a fresh install of dependencies we will be using this to work with all the req deps from now on

For DBow2:
change all instances of
#include <opencv/cv.h>
to
#include <opencv2/opencv.hpp>

use pangolin 0.5, default is 0.9

git clone https://github.com/chintha/U-VIP-SLAM.git USLAM

$ git clone https://github.com/catchorg/Catch2.git
$ cd Catch2
$ cmake -Bbuild -H. -DBUILD_TESTING=OFF


$ sudo cmake --build build/ --target install 

use catch2 v2.x
if still fail, remove all catch2 instances from install_prerequisites.sh

https://github.com/raulmur/ORB_SLAM2/issues/1015

ensure you export ur installed packages in and source ur ~/.bashrc

if
cmake .. -DROS_BUILD_TYPE=Release
doesnt work, run this instead:
cmake .. -DROS_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYTHON_INCLUDE_DIR=/usr/include/python3.8

-DCMAKE_INSTALL_PREFIX=/usr/local


for U-VIP-SLAM include .h files:
change all instances of
#include <opencv/cv.h>
to
#include <opencv2/opencv.hpp>


for error 'cv_filled' was not declared in this scope: OpenCV4 is unsupported
either downgrade to Opencv3.4.6:
wget -O opencv.zip https://github.com/opencv/opencv/archive/3.4.6.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.6.zip
mkdir -p build && cd build
cmake -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib-3.4.6/modules ../opencv-3.4.6

or use updated fork here

for error rospack found package at "" but the current dir is ...
Ur ROS_PACKAGE_PATH is probably incorrect, ensure it is in the correct order as well (e.g. ur build folder root should be before the ros/noetic/share)


Pangolin 0.4 installation:
in src/CMakeLists.txt, remove FFMPEG api
make n build according to instructions +
sudo apt install liblapack-dev  libopenblas-dev

for error: /usr/bin/ld: cannot find -lEigen3::Eigen
add to cmakelists: -lopencv_imgproc -lopencv_core -lopencv_imgcodecs
list(APPEND CMAKE_INCLUDE_PATH "/usr/local/include") 
find_package (Eigen3 3.3 REQUIRED NO_MODULE)
create symlinks for /usr/lib/x86_64-linux-gnu files libopencv_core.so, libopencv_imgcodecs.so, libopencv_imgproc.so files and the 4.2.x versions to /usr/lib (sudo ln -s)
force CMake to find_package(OpenCV 4 REQUIRED)

Running e.g.:
rosrun USLAM USLAM Data/ORBvoc.txt Data/Settings_VI_Aqualoc_harbor.yaml
