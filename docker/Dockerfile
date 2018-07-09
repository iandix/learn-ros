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
# Install VSCode & Core Plugins
# --------------------------------------------------------------------------
# Note:
#   Although we have installed VSCode 64 bits, it requires
#   some 32 bits library:
#       dpkg --add-architecture i386 - enables 32 bits architecture
#       libgtk2.0-0:i386 - 32 bits lib required by VSCode
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y libgtk2.0-0:i386
RUN wget -O code.deb 'https://go.microsoft.com/fwlink/?LinkID=760868' && \
    apt install -y ./code.deb && \
    rm -f code.deb

RUN mkdir /root/.vscode && \
    code \
    --user-data-dir="/root/.vscode" \
    --install-extension ms-python.python

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

CMD [ "gazebo" ]
#TBD Print msg at start: 'To launch VSCode as root you have to use --user-data-dir="/root/.vscode"'