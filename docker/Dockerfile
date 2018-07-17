FROM ros:kinetic-ros-base
LABEL maintainer="ianaguidinix@gmail.com"

# --------------------------------------------------------------------------
# Install bootstrap tools
# --------------------------------------------------------------------------
RUN apt-get update
RUN apt-get install --no-install-recommends -y ros-kinetic-gazebo-* 
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc

# --------------------------------------------------------------------------
# Install ROS packages
# --------------------------------------------------------------------------
RUN apt-get update && \
    apt-get install -y \
        ros-kinetic-ros-tutorials \
        ros-kinetic-rqt \
        ros-kinetic-rqt-common-plugins \
        ros-kinetic-turtle-tf2 \
        ros-kinetic-tf2-tools \
        ros-kinetic-tf

# --------------------------------------------------------------------------
# General purpose tools
# --------------------------------------------------------------------------
RUN apt-get install -y --no-install-recommends \
    curl \
    wget \
    unzip \
    git \
    evince \
    vim

# --------------------------------------------------------------------------
# Cleaning up
# --------------------------------------------------------------------------
RUN apt-get autoremove -y && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/*   

# --------------------------------------------------------------------------
# nvidia-docker hooks
# --------------------------------------------------------------------------
LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV PATH /usr/local/nvidia/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}

CMD [ "gazebo", "--verbose" ]
