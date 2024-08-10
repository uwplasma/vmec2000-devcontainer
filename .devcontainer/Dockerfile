# Use an official base image with a compatible OS
FROM ubuntu:20.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && \
    apt-get install -y \
    git \
    python3 \
    python3-pip \
    build-essential \
    cmake \
    libnetcdf-dev \
    netcdf-bin \
    libopenblas-dev \
    liblapack-dev \
    libscalapack-mpi-dev \
    mpi-default-bin \
    mpi-default-dev

RUN apt-get update && \
apt-get install -y \
libnetcdff-dev

# Install Python packages
RUN pip3 install --upgrade pip && \
    pip3 install numpy cmake scikit-build ninja f90wrap

# Set the working directory
WORKDIR /vmec2000

# Clone the VMEC2000 repository
RUN git clone https://github.com/hiddenSymmetries/VMEC2000.git /vmec2000

# Set the working directory to the cloned repository
WORKDIR /vmec2000

# Replace the default CMake configuration file with the one for Ubuntu since
# the docker image being used is based on Ubuntu
RUN cp cmake/machines/ubuntu.json cmake_config_file.json

# Set environment variables for NetCDF
ENV NETCDF_INC_PATH=/usr/include
ENV NETCDF_LIB_PATH=/usr/lib/x86_64-linux-gnu

# Build and install the VMEC2000 Python extension
RUN pip install numpy 

RUN python3 -m pip install . 

# Default command to start an interactive Python shell when the container starts
CMD ["python3"]