# Build Guide

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

  sh install.sh elixir@1.17.3 otp@27.1.2
  installs_dir=$HOME/.elixir-install/installs
  export PATH=$installs_dir/otp/27.1.2/bin:$PATH
  export PATH=$installs_dir/elixir/1.17.3-otp-27/bin:$PATH
  iex
  ```

  ```bash
  sudo apt update && sudo apt install -y elixir
  ```

- Install xsltproc and xmlto

  ```bash
  sudo apt update && sudo apt install -y xsltproc xmlto
  ```

## Reference

- [How do I install erlang OTP 25 on ubuntu? - Stack Overflow](https://stackoverflow.com/questions/74390581/how-do-i-install-erlang-otp-25-on-ubuntu)
- [Server Build Instructions | RabbitMQ](https://www.rabbitmq.com/docs/build-server)
