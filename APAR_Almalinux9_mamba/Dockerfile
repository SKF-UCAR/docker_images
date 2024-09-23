# Use your local AlmaLinux 9-based image as the base
FROM APAR_Almalinux9:latest

# Set environment variables for Conda and Mamba
ENV PATH /opt/conda/bin:$PATH
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Install dependencies for Conda and Mamba using AlmaLinux package manager (dnf)
RUN dnf update -y && \
    dnf install -y \
    wget \
    bzip2 \
    ca-certificates \
    git \
    libXrender \
    libSM \
    libXext \
    glibc && \
    dnf clean all && \
    rm -rf /var/cache/dnf

# Download and install Miniconda (or replace with Anaconda if needed)
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh && \
    bash miniconda.sh -b -p /opt/conda && \
    rm miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

# Install Mamba, which provides a faster package manager than Conda
RUN /opt/conda/bin/conda install mamba -n base -c conda-forge && \
    /opt/conda/bin/conda clean -afy

# Create a new environment with Python 3.10+
RUN /opt/conda/bin/mamba create -n myenv python=3.10 -c conda-forge && \
    /opt/conda/bin/conda clean -afy

# Activate the environment (for bash shells)
SHELL ["bash", "-c"]
RUN echo "source activate myenv" > ~/.bashrc
ENV PATH /opt/conda/envs/myenv/bin:$PATH

# Set the working directory in the container
WORKDIR /app

# Copy local application code into the container
COPY . /app

# Install Python dependencies if necessary (use requirements.txt if available)
# Uncomment and modify if applicable:
# RUN mamba install --name myenv --file requirements.txt && mamba clean -afy

# Set the default command to run your application
# CMD ["python", "your_application.py"]
