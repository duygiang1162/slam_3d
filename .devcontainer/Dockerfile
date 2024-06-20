FROM osrf/ros:humble-desktop

# Add vscode user with same UID and GID as your host system
# (copied from https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user)
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

# Install Git
RUN sudo apt install -y git
 ######################################################################## ADD #########################################################################
# Install Gazebo Simualtor
RUN sudo apt install gazebo -y
RUN sudo apt install ros-humble-gazebo-ros-pkgs -y

# Install ROS2 Dependent Packages
#Cartographer
RUN sudo apt install ros-humble-cartographer -y
RUN sudo apt install ros-humble-cartographer-ros -y

#Navigation Stack
RUN sudo apt install ros-humble-navigation2 -y 
RUN sudo apt install ros-humble-nav2-bringup -y

# Install RQT
RUN sudo apt install ros-humble-rqt* -y

# Install XACRO 
RUN sudo apt install ros-humble-xacro -y 

# Rosdep update
RUN rosdep update


# Install Join state Publisher
RUN sudo apt-get install ros-humble-joint-state-publisher-gui -y 

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
RUN echo 'export TURTLEBOT3_MODEL=burger' >> ~/.bashrc
RUN echo "alias rb='colcon build && source install/setup.bash && echo \"Build and Source Completed------------------\"'" >> ~/.bashrc
RUN source ~/.bashrc