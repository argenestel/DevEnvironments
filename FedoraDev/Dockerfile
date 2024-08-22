# Start with the latest Fedora base image
FROM fedora:latest

# Update the system and install necessary packages
RUN dnf update -y && dnf install -y \
    git \
    zsh \
    neovim \
    cargo \
    rust \
    python3 \
    python3-pip \
    nodejs \
    npm \
    curl \
    wget \
    gcc \
    g++ \
    make \
    sudo \
    && dnf clean all

# Set up Oh My Zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# Install NvChad
RUN git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1

# Set Zsh as the default shell
RUN chsh -s $(which zsh)

# Create a non-root user for development and add to sudo group
RUN useradd -m -s /bin/zsh developer && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Set up Oh My Zsh for the developer user
USER developer
WORKDIR /home/developer
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Set up environment variables
ENV SHELL=/bin/zsh
ENV TERM=xterm-256color

# Start Zsh when the container runs
CMD [ "zsh" ]
