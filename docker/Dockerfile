# Image

# Pull the image
FROM osrf/ros:noetic-desktop-full

# Change to bash
SHELL ["/bin/bash", "-c"]

# Install ubuntu packages
COPY third_party/china.list /etc/apt/sources.list
RUN apt-get update 
RUN apt install -y wget \
                   curl \
                   gnupg \
                   vim \
                   software-properties-common \
                   git \
                   python3-wstool \
                   python3-rosdep \
                   ninja-build \
                   stow \
                   python3-pip


RUN apt install -y ros-noetic-cv-bridge \
                   ros-noetic-tf \
                   ros-noetic-message-filters \
                   ros-noetic-image-transport \
                   ros-noetic-image-transport* \
                   ros-noetic-realtime-tools \
                   ros-noetic-joint-state-controller \
                   ros-noetic-twist-mux \
                   ros-noetic-velocity-controllers \
                   ros-noetic-map-server \
                   ros-noetic-amcl \
                   ros-noetic-gmapping \
                   ros-noetic-hector-trajectory-server 

# Install third party dependencies
# PCLlib libpcl-dev
RUN add-apt-repository ppa:borglab/gtsam-release-4.0
RUN apt update 
RUN apt install -y libcgal-dev \
                   libeigen3-dev \
                   libsuitesparse-dev \
                   libpcl-dev \
                   python3-sphinx


# FAST-LIO packages
COPY third_party/Livox-SDK-master /root/Livox-SDK-master
WORKDIR /root/Livox-SDK-master
RUN cd  /root/Livox-SDK-master/build && \
    cmake .. && \
    make && \
    make install

# Create a ROS working space
RUN mkdir -p /root/catkin_ws
WORKDIR /root/catkin_ws

# Set ROS in .bashrc
RUN echo source /opt/ros/noetic/setup.bash >> /root/.bashrc
RUN echo source /root/catkin_ws/install_isolated/setup.bash >> /root/.bashrc

# Clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get clean && apt autoclean