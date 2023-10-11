# Use the base image for riscv64/ubuntu
FROM riscv64/ubuntu

# Set environment variables for the user account
ENV USER_NAME ace5g
ENV HOME /home/$USER_NAME

# RUN passwd -d root
# Create a user account named "ace5g" without a password
RUN useradd -m ace5g && passwd -d ace5g 
# RUN usermod -aG sudo ace5g

# Install required packages (C++, Rust, Emacs, CMake)
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    curl \
    sudo \ 
    build-essential \
    git \
    python3 python3-pip \
    emacs \
    ninja-build \
    cmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Switch to the non-root user
USER $USER_NAME

# Set the working directory to the user's home directory
WORKDIR $HOME

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs >> install-rust.sh && sh ./install-rust.sh -y && rm install-rust.sh && echo 'source $HOME/.cargo/env' >> /home/ace5g/.bashrc &&  ./.cargo/bin/rustup target install wasm32-wasi

# Entry point (start a shell by default)
CMD ["/bin/bash"]

