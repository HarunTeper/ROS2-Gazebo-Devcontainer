# ROS2-Gazebo-Devcontainer

## Setup

Install [Docker Engine](https://docs.docker.com/engine/install/)

Install [Visual Studio Code](https://code.visualstudio.com/)

## Start the Container with Visual Studio Code

In Visual Studio Code, install the **Docker** and **Dev Containers** extensions.

Build and open the container.

## Start the Container with Docker

Run the following command in a terminal that is in the current folder's directory:

> docker build -t ros2-gazebo .devcontainer/

Start the container using the following command:

> docker run --network host -it -v .:/home/vscode/workspace ros2-gazebo
