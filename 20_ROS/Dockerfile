FROM osrf/ros:kilted-desktop-full-noble

ENV DEBIAN_FRONTEND=noninteractive

# Update base system
RUN apt update && apt upgrade -y

# ROS 2 development tools and common robotics packages
RUN apt update && apt install -y \
    # Build tools
    build-essential \
    cmake \
    git \
    wget \
    curl \
    nano \
    vim \
    python3-pip \
    python3-colcon-common-extensions \
    python3-rosdep \
    
    ros-kilted-ros-gz    \
    # ROS 2 build/debug tools
    ros-kilted-rqt \
    ros-kilted-rqt-common-plugins \
    ros-kilted-ros2-control \
    ros-kilted-ros2-controllers \
    \
    # Robot description
    ros-kilted-robot-state-publisher \
    ros-kilted-joint-state-publisher \
    ros-kilted-joint-state-publisher-gui \
    ros-kilted-xacro \
    \
    # Navigation for mobile robots
    ros-kilted-navigation2 \
    ros-kilted-nav2-bringup \
    \
    # # SLAM
    # ros-kilted-slam-toolbox \
    \
    # # Localization
    # ros-kilted-robot-localization \
    \
    # TF tools
    ros-kilted-tf2-tools \
    ros-kilted-tf-transformations \
    \
    # MoveIt for robot arms/manipulators
    ros-kilted-moveit \
    \
    # Common sensors
    ros-kilted-image-transport \
    ros-kilted-camera-info-manager \
    ros-kilted-cv-bridge \
    # ros-kilted-pointcloud-to-laserscan \
    \
    # ROS testing tools
    # ros-kilted-ros-testing \
    # ros-kilted-ament-cmake \
    \
    # Useful Python robotics packages
    python3-numpy \
    python3-opencv \
    python3-yaml \
    \
    && rm -rf /var/lib/apt/lists/*

RUN sudo apt-get update && sudo apt-get install curl lsb-release gnupg
RUN sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] https://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null \
    sudo apt-get update \
    sudo apt-get install gz-jetty

# Initialize rosdep
RUN rosdep init || true && \
    rosdep update


# Default workspace
WORKDIR /ros2_ws


# Automatically source ROS when opening a shell
RUN echo "source /opt/ros/kilted/setup.bash" >> /root/.bashrc
RUN echo "source /ros2_ws/install/setup.bash 2>/dev/null || true" >> /root/.bashrc


CMD ["bash"]