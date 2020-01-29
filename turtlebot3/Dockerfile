FROM ros2:dashing

MAINTAINER tygoto <tygoto@me.com>

RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    google-mock \
    libceres-dev \
    liblua5.3-dev \
    libboost-dev \
    libboost-iostreams-dev \
    libprotobuf-dev \
    protobuf-compiler \
    libcairo2-dev \
    libpcl-dev \
    python3-sphinx \
    sudo

# RUN curl -sSL http://get.gazebosim.org | sh

RUN sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
RUN wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    gazebo9 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*


RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    ros-dashing-gazebo-* \
    ros-dashing-cartographer \
    ros-dashing-cartographer-ros \
    ros-dashing-navigation2 \
    ros-dashing-nav2-bringup \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN . /opt/ros/$ROS_DISTRO/setup.sh \
 && mkdir -p /turtlebot3_ws/src \
 && cd /turtlebot3_ws \
 && wget https://raw.githubusercontent.com/ROBOTIS-GIT/turtlebot3/ros2/turtlebot3.repos \
 && vcs import src < turtlebot3.repos \
 && colcon build --symlink-install

ARG DOCKER_UID=1000
ARG DOCKER_USER=turtle
ARG DOCKER_PASSWORD=bot
RUN useradd -m --uid ${DOCKER_UID} --groups sudo ${DOCKER_USER} \
 && echo ${DOCKER_USER}:${DOCKER_PASSWORD} | chpasswd
USER ${DOCKER_USER}

RUN echo "source /opt/ros/dashing/setup.bash" >> ~/.bashrc \
 && echo "source /turtlebot3_ws/install/setup.bash" >> ~/.bashrc

CMD ["bash"]