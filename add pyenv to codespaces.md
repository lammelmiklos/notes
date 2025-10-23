```bash
sudo apt update
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncursesw5-dev libncurses5-dev xz-utils tk-dev \
    libffi-dev liblzma-dev python3-openssl git

curl https://pyenv.run | bash
```

And add this to .bashrc file so it is there for every startup

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"

# Load pyenv automatically
eval "$(pyenv init --path)"
eval "$(pyenv init -)"

# (Optional) If you use the plugin pyenv-virtualenv:
eval "$(pyenv virtualenv-init -)"
```


# Use pyenv for different versions & projects

To install a Python version:

```bash
pyenv install <version>
```

To set the global default version for your user:
```bash
pyenv global <version>
```

To set a version locally for a particular project directory (creates a .python-version file):
```bash
cd /path/to/project
pyenv local <version>
```

To revert to the system Python (the one Ubuntu shipped):
```bash
pyenv global system
```
