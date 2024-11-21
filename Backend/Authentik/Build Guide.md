# Build Guide

this build environment is create using ubuntu in docker

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
- Install `nvm`

  - Install `nvm` using script , the version number can be change

    ```shell
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
    ```

  - Add following script to `~/.bashrc`

    ```shell
    echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.bashrc
    echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion' >> ~/.bashrc
    ```

  - `source ~/.bashrc`

- Install Node.js using `nvm`
  - `nvm install 22`
  - `nvm use 22`
- Install `poetry` using `pip`
  - `pip install poetry`
- Install `go`
  - `wget https://go.dev/dl/go1.23.3.linux-amd64.tar.gz`
  - `rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz`
  - `echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc`
- Install other dependencies
  - `apt install libkrb5-dev libpq-dev -y`
- Install `postgresql` , this is optional

  - `apt install -y postgresql postgresql-contrib`
  - `service postgresql restart`
  - Create database and user to postgres
    - `sudo -i -u postgres`
    - `psql`
    - `CREATE DATABASE database_name;`
    - `CREATE USER myuser WITH PASSWORD 'mypassword';`
    - `GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;`
  - Add Evnironment

  ```bash
  export AUTHENTIK_POSTGRESQL__HOST=localhost
  export AUTHENTIK_POSTGRESQL__NAME=authentik
  export AUTHENTIK_POSTGRESQL__USER=myuser
  export AUTHENTIK_POSTGRESQL__PORT=5432
  export AUTHENTIK_POSTGRESQL__PASSWORD=mypassword
  ```

- Install `redis`
  - `apt install redis -y`
  - `service redis-server restart`

Before building the project, I will change the `npm` command to `yarn` because `npm` gets stuck while running `npm ci`. This problem occurs because the `package.json` file uses the wrong name for the dependency package `@esbuild/linux-amd64`. We need to change in to `@esbuild/linux-x64` in `web\package.json`, but i still recommend using another package manager.

## Build Project

- `poetry shell`
- `make install`
- `make gen-dev-config`
- `make web-build`
- `lifecycle/ak server`

## Reference

- [Full development environment | authentik](https://docs.goauthentik.io/docs/developer-docs/setup/full-dev-environment)
