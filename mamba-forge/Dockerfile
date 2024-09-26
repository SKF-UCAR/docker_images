# Start from the official mambaforge image
FROM mambaforge:latest

# Set up environment variables for non-interactive installation
ENV DEBIAN_FRONTEND=noninteractive

# Install base OS dependencies required for building C++ packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    git \
    g++ \
    make \
    libtool \
    autoconf \
    pkg-config \
    curl \
    wget \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Create a working directory
WORKDIR /workspace

# Create a new conda environment with essential base packages for C++ development
RUN mamba create -n cpp_build_env -y \
    compilers \
    cmake \
    automake \
    autoconf \
    libtool \
    pkg-config \
    gxx_linux-64 \
    make \
    conda-build \
    conda-forge::mamba

# Activate the conda environment and add the environment to the PATH
SHELL ["conda", "run", "-n", "cpp_build_env", "/bin/bash", "-c"]

# Set up the conda environment as the default shell
RUN echo "conda activate cpp_build_env" >> ~/.bashrc

# Expose the workspace directory (optional)
VOLUME /workspace

# Default command to run bash
CMD ["/bin/bash"]
