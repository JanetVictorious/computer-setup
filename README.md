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

Install the following software via homebrew
- pipenv

---

## Setup conda environment

Install [Conda](https://www.anaconda.com/products/individual).

Follow the instructions to initialize conda.  
Setup python environments and install `pip-tools`:
```shell
$ conda create --name python-3.X python=3.X
$ conda activate python-3.X
$ pip install pip-tools
```

> If you rather use pipenv instead of conda a similar procedure can be done.

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

---

## Install Terraform

```shell
$ brew install tfenv
$ tfenv list-remote
$ tfenv install <terraform version>
$ tfenv use <terraform version>
```
