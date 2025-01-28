## U-VIP-SLAM Implementation for ROS Noetic

#### Deviations from U-VIP-SLAM (to be updated):
- updated all headers from opencv to opencv2
- updated pangolin dependency from 0.5 to 0.9
- removed catch2 instances from install_prerequisites.sh
- added flags to CMakeLists:
  - -lopencv_imgproc -lopencv_core -lopencv_imgcodecs
  - find_package (Eigen3 3.3 REQUIRED NO_MODULE)
  - find_package(OpenCV 4 REQUIRED)

#### Running example:
`rosrun USLAM USLAM Data/ORBvoc.txt Data/Settings_VI_Aqualoc_harbor.yaml`
