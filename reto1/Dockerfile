FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Instalación como root
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget curl git bash ca-certificates && \
    wget https://github.com/yudai/gotty/releases/download/v1.0.1/gotty_linux_amd64.tar.gz && \
    tar -xvzf gotty_linux_amd64.tar.gz && \
    mv gotty /usr/local/bin/ && \
    rm -rf gotty_linux_amd64.tar.gz

# Crear usuario y cambiar permisos
RUN useradd -ms /bin/bash ctfuser

RUN apt-get install -y zsh git fonts-powerline && \
    su - ctfuser -c "sh -c \"\$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)\" --unattended" && \
    sed -i 's/ZSH_THEME=".*"/ZSH_THEME="robbyrussell"/g' /home/ctfuser/.zshrc && \
    chsh -s /bin/zsh ctfuser


USER ctfuser
WORKDIR /home/ctfuser

COPY flag.txt /home/ctfuser/flag.txt

# Comando final
CMD ["gotty", "--port", "8080", "--permit-write", "zsh"]

