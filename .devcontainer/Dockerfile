ARG VARIANT=ubuntu-22.04
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# --- Configure environment ---

# Configure DEBIAN_FRONTEND to avoid warnings
ENV DEBIAN_FRONTEND=noninteractive

# set up work directory
WORKDIR /home/vscode/workspace

# --- Install ROS2 ---

# install locales for UTF-8 support
RUN apt-get update && apt-get install -y locales && \
    locale-gen en_US.UTF-8 && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

# set locale environment variables
ENV LANG=en_US.UTF-8

# add ROS2 repository
RUN apt-get update && \
    apt-get install -y software-properties-common curl git && \
    add-apt-repository universe && \
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

# install ROS2
RUN apt-get update && \
    apt-get install -y ros-humble-desktop

# install ROS2 development tools
RUN apt-get -y install python3-pip python3-colcon-common-extensions

# --- Install Gazebo ---

# install Gazebo
RUN sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list' && \
    wget https://packages.osrfoundation.org/gazebo.key -O - | apt-key add - && \
    apt-get update && \
    apt-get install -y gazebo

# install Gazebo ROS packages
RUN apt-get install -y ros-humble-gazebo-ros-pkgs

# Expose the Gazebo port
EXPOSE 11345

# --- Install DevTools ---

RUN apt-get update && \
    apt-get -y install clangd clang-format clang-tidy cppcheck && \
    pip install pep8 pylint

# --- Set up user ---

# set user
USER vscode

# source ROS2 setup file
RUN echo '. /opt/ros/humble/setup.sh' >> /home/vscode/.bashrc

# configure environment variables
ENV DISPLAY=unix:1
ENV ROS_LOCALHOST_ONLY=0
ENV ROS_DOMAIN_ID=0

# --- Set up entrypoint ---

SHELL ["/bin/bash", "-c"]