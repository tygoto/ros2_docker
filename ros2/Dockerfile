FROM ubuntu:bionic

MAINTAINER tygoto <tygoto@me.com>

RUN DEBIAN_FRONTEND=noninteractive
ENV DEBCONF_NOWARNINGS=yes
ENV TZ Asia/Tokyo
ENV ROS_DISTRO dashing
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    tzdata \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    build-essential \
    cmake \
    curl \
    ca-certificates \
    git \
    gnupg2 \
    lsb-release \
    python3-pip \
    wget \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
RUN echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list

RUN apt-get update \ 
 && apt-get install -q -y --no-install-recommends \
    ros-dashing-desktop \
    python-rosdep \
    python3-argcomplete \
    python3-colcon-common-extensions \
    python3-vcstool \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY ./entrypoint.sh /
RUN ["chmod", "+x", "/entrypoint.sh"]
ENTRYPOINT ["/entrypoint.sh"]

CMD ["bash"]
