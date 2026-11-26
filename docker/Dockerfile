# Author: TaeYoung Kim
# email: tyoung96@yonsei.ac.kr

FROM osrf/ros:humble-desktop-full-jammy

# Install PCL & Eigen & essential libraries
RUN apt-get update && apt-get install -y cmake libatlas-base-dev libeigen3-dev libpcl-dev libgoogle-glog-dev libsuitesparse-dev libglew-dev wget unzip git python3-pip
RUN apt-get install -y ros-humble-tf2 ros-humble-cv-bridge ros-humble-pcl-conversions ros-humble-xacro ros-humble-robot-state-publisher \
    ros-humble-rviz2 ros-humble-image-transport ros-humble-image-transport-plugins ros-humble-pcl-ros

# Install matplotlib
RUN apt-get update && apt-get install -y libtbb-dev python-tk && pip install matplotlib 

# Install ceres-solver
WORKDIR /root/thirdParty
RUN wget https://github.com/ceres-solver/ceres-solver/archive/refs/tags/2.1.0.tar.gz
RUN tar zxf 2.1.0.tar.gz
WORKDIR /root/thirdParty/ceres-solver-2.1.0
RUN mkdir build
WORKDIR /root/thirdParty/ceres-solver-2.1.0/build
RUN cmake -DCMAKE_BUILD_TYPE=Release .. && make -j4 && make install


WORKDIR /root/ros2_ws

# Load ROS environment at each run
COPY ./ros_entrypoint.sh /
RUN chmod 755 /ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

CMD ["bash"]
