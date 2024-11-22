# Build Guide

- Install `pyenv`

  - install dependencies

    ```shell
    apt update && apt install -y make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
    liblzma-dev python3-openssl git
    ```

  - install pyenv by script  
    `curl https://pyenv.run | bash`
  - Add following text to `~/.bashrc`

    ```shell
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc
    ```

  - refresh `~/.bashrc` by `source ~/.bashrc`

- Install python by using `pyenv`
  - `pyenv install 3.12.4` (you can choose your python version to install)
  - `pyenv global 3.12.4`
- Install evm to manage erlang

  - install using following commands

  ```git
  git clone https://github.com/robisonsantos/evm /tmp/evm/
  cd /tmp/evm/
  /tmp/evm/install
  echo 'source ~/.evm/scripts/evm' >> ~/.bashrc
  source ~/.bashrc
  ```

- Install Erlang using evm

  ```bash
  evm install 26.2 -y
  evm default 26.2
  ```

- Install erlang-nox , erlang-dev

  ```bash
  apt install -y erlang-nox erlang-dev
  ```

- Install elixir
  - `apt update && apt install -y elixir`
- Install xsltproc and xmlto
  - `apt update && apt install -y xsltproc xmlto`

## Reference

- [How do I install erlang OTP 25 on ubuntu? - Stack Overflow](https://stackoverflow.com/questions/74390581/how-do-i-install-erlang-otp-25-on-ubuntu)
