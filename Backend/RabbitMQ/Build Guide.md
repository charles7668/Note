# Build Guide

- [Build Guide](#build-guide)
  - [Build Manually](#build-manually)
  - [Dockerfile to build env](#dockerfile-to-build-env)
  - [Reference](#reference)

## Build Manually

- Install `pyenv`

  - install dependencies

    ```bash
    sudo apt update && sudo apt install -y make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
    liblzma-dev python3-openssl git
    ```

  - install pyenv by script

    ```bash
    curl https://pyenv.run | bash
    ```

  - Add following text to `~/.bashrc`

    ```bash
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc
    ```

  - refresh `~/.bashrc`

    ```bash
    source ~/.bashrc
    ```

- Install python by using `pyenv` (you can choose your python version to install)

  ```bash
  pyenv install 3.12.4
  pyenv global 3.12.4
  ```

- Install evm to manage erlang

  - install using following commands

    ```bash
    CURRENT_DIR=$(pwd)
    git clone https://github.com/robisonsantos/evm /tmp/evm/
    cd /tmp/evm/
    /tmp/evm/install
    echo 'source ~/.evm/scripts/evm' >> ~/.bashrc
    source ~/.bashrc
    cd "$CURRENT_DIR"
    ```

- Install Erlang using evm
  - before use install , make sure unzip is installed

    ```bash
    sudo apt install zip unzip -y
    ```

  - Install erlang using evm

    ```bash
    evm install 26.2 -y
    evm default 26.2
    ```

- Install erlang-nox , erlang-dev

  ```bash
  sudo apt install -y erlang-nox erlang-dev
  ```

- Install elixir

  ```bash
  curl -fsSO https://elixir-lang.org/install.sh

  sh install.sh elixir@1.17.3 otp@26.2
  echo 'export PATH=$HOME/.elixir-install/installs/otp/26.2/bin:$PATH' >> ~/.bashrc
  echo 'export PATH=$HOME/.elixir-install/installs/elixir/1.17.3-otp-26/bin:$PATH' >> ~/.bashrc
  source ~/.bashrc
  ```

- Install xsltproc and xmlto

  ```bash
  sudo apt update && sudo apt install -y xsltproc xmlto
  ```

## Dockerfile to build env

```Dockerfile
FROM ubuntu:22.04

USER root

RUN echo "Asia/Taipei" | tee /etc/timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime

RUN apt update && apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
liblzma-dev python3-openssl git zip unzip

RUN curl https://pyenv.run | bash
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
RUN echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc
RUN export PYENV_ROOT="$HOME/.pyenv" && \
    [ -d $PYENV_ROOT/bin ] && export PATH="$PYENV_ROOT/bin:$PATH" && \
    eval "$(pyenv init -)" && \
    pyenv install 3.12.4 && \
    pyenv global 3.12.4

RUN bash -c "CURRENT_DIR=$(pwd) && \
    git clone https://github.com/robisonsantos/evm /tmp/evm/ && \
    cd /tmp/evm/ && \
    /tmp/evm/install && \
    echo 'source ~/.evm/scripts/evm' >> ~/.bashrc && \
    source ~/.evm/scripts/evm && \
    evm install 26.2 -y && \
    evm use 26.2"
RUN apt install -y erlang-nox erlang-dev

RUN curl -fsSO https://elixir-lang.org/install.sh && \
    sh install.sh elixir@1.17.3 otp@26.2 && \
    echo 'export PATH=$HOME/.elixir-install/installs/otp/26.2/bin:$PATH' >> ~/.bashrc && \
    echo 'export PATH=$HOME/.elixir-install/installs/elixir/1.17.3-otp-26/bin:$PATH' >> ~/.bashrc

RUN apt update && apt install -y xsltproc xmlto

RUN apt update && apt install -y openssh-server

RUN mkdir -p /run/sshd

RUN sed -i 's/^#*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config

RUN echo 'root:0000' | chpasswd

CMD ["/usr/sbin/sshd", "-D"]

EXPOSE 22
```

## Reference

- [How do I install erlang OTP 25 on ubuntu? - Stack Overflow](https://stackoverflow.com/questions/74390581/how-do-i-install-erlang-otp-25-on-ubuntu)
- [Server Build Instructions | RabbitMQ](https://www.rabbitmq.com/docs/build-server)
