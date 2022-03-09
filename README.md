# Janets macOS setup

## Terminal

Download [iterm2](https://iterm2.com/)

Set preferences
- Color theme: `Preferences` -> `Profiles` -> `Colors` -> `Color Presets...` -> `Solarized Dark`

---

## oh-my-zsh

Install [oh-my-zsh](https://ohmyz.sh/)

Add the following [plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins):
- git
- gitfast
- z
- zsh-autosuggestions (manual git clone, see guide [here](https://github.com/zsh-users/zsh-autosuggestions))

---

## Package manager

Install [Homebrew](https://brew.sh/).

Install the following software via homebrew:
- `pipenv`

- `terraform` & `tfenv`

    ```shell
    $ brew install terraform
    > This downloads terraform

    $ brew install tfenv
    > In-case you get a linking error, run the following:

    $ brew unlink terraform && brew install tfenv && brew link terraform

    $ tfenv list-remote
    $ tfenv install <terraform version>
    $ tfenv use <terraform version>

    $ tfenv --version
    $ terraform --version
    ```

---

## Install docker

Install [docker desktop](https://www.docker.com/products/docker-desktop)

---

## (Option 1: mac intel chip) - Setup conda environment

Install [Conda](https://www.anaconda.com/products/individual).

Follow the instructions to initialize conda.  
Setup python environments and install `pip-tools`:
```shell
# Create specific python environment
$ conda create --name python-3.X python=3.X
$ conda activate python-3.X

# Upgrade pip to latest version
$ pip install --upgrade pip

# Install pip-tools
$ pip install pip-tools
```

## (Option 2: macOS ARM64 chip) - Setup pyenv

New mac computers with M1 (ARM64) chip run on a different architecture and some difficulties can occur if you're using conda. By using `pyenv` we can create environments and pip to install native macOS ARM64 wheels or build packages from source.  

Follow this [installation guide](https://github.com/pyenv/pyenv#installation) on Github to set up `pyenv`.

---

## Generate ssh-key

Follow the [guide on Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for generating a new SSH key and adding it to the ssh-agent.  

The following snippet can be added to `.zshrc` in order to handle mutilple git accounts:
```shell
$ # SSH initialize
$ function start_agent {
$     echo "Initialising new SSH agent..."
$     /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
$     echo succeeded
$     chmod 600 "${SSH_ENV}"
$     . "${SSH_ENV}" > /dev/null
$     /usr/bin/ssh-add;
$ }

$ if [ -f "${SSH_ENV}" ]; then
$     . "${SSH_ENV}" > /dev/null
$     #ps ${SSH_AGENT_PID} doesn't work under cywgin
$     ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
$         start_agent;
$     }
$ else
$     start_agent;
$ fi
```

**Note:** Github suggest HTTPS over SSH for various reasons. Some comments from Github:
> Sometimes, firewalls refuse to allow SSH connections entirely. If using [HTTPS cloning with credential caching](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git) is not an option, you can attempt to clone using an SSH connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere.

Using [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager) (GCM) you can store your credentials securely and connect to GitHub over HTTPS.

---

## Download VS Code

Go to this [website](https://code.visualstudio.com/) and follow the instructions for downloading VS code.
