# Use the official Alma Linux 9 base image
FROM almalinux:9

RUN dnf update -y

# Install environment groups
RUN dnf group install  -y --allowerasing "Server" "Workstation"

# Install developer tools group
RUN dnf group install -y --allowerasing "Development Tools" 

# Install tools needed for LROSE
RUN dnf install -y epel-release
RUN dnf install -y 'dnf-command(config-manager)'

# install generic tools 
RUN dnf install -y \
    tcsh wget git \
    emacs rsync python mlocate \
    python-devel platform-python-devel \
    m4 make cmake libtool autoconf automake \
    gcc gcc-c++ gcc-gfortran glibc-devel
RUN dnf install -y --allowerasing \
    libX11-devel libXext-devel libcurl-devel \
    libpng-devel libtiff-devel zlib-devel libzip \
    expat-devel libcurl-devel openmpi-devel \
    xorg-x11-xauth \
    flex fftw3-devel bzip2-devel 

# install project related libs 
RUN dnf install -y --allowerasing \
    qt6-qtbase-devel qt6-qtdeclarative-devel \
    qt6-qtserialport-devel qt6-qtremoteobjects-devel \
    log4cpp-devel gtest-devel boost-devel \
    hdf5-devel netcdf-devel \
    rpm-build redhat-rpm-config \
    rpm-devel rpmdevtools socat

# Clean up package manager cache
RUN dnf clean all

# Create a user with the provided username and password
ARG USERNAME=apar
ARG PASSWORD=pa$$w0rd
RUN useradd -m -p $(openssl passwd -1 $PASSWORD) $USERNAME
# adding user to sudo group
RUN usermod -aG wheel ${USERNAME}

# Set the working directory
WORKDIR /home/${USERNAME}
USER ${USERNAME}
RUN mkdir ./.ssh
VOLUME ["/home/${USERNAME}/.ssh"]


RUN mkdir ./projects
VOLUME [ "/home/${USERNAME}/projects" ]

WORKDIR /home/${USERNAME}/projects


# Define default command or entry point if needed
CMD ["/bin/bash"]