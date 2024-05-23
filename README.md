# Dev Day 2: Setup Your Environment

## Step 1: WSL

Before installing we need to enable the following features in powershell. Open powershell with administrator privileges.

``` powershell
# Enable Virtual Machine Platform
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

# Enable Windows Subsystem for Linux
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# Enable Hyper-V
dism.exe /online /enable-feature /featurename:Microsoft-Hyper-V-All /all /norestart

# Restart the computer to apply changes
Restart-Computer
```

Install WSL:

``` powershell
wsl --set-default-version 2
wsl --update
wsl --install -d Ubuntu
```

Then restart your machine and wait for installation to complete.

It will then prompt you for a new username and password. I recommend setting the username to the same as your window system.

``` text
Ubuntu is already installed.
Launching Ubuntu...
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: kristian
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
```

WSL is successfully installed!

## Step 2: VSCode Install and Setup

Download, install and open VSCode from [here](https://code.visualstudio.com/).

On the left hand bar find the extensions tab. Here we can install the `remote wsl` extension to allow VSCode to connect to the WSL container directly.

Useful extensions to install:

``` text
python (ms-python.python)
gitlens (eamodio.gitlens)
code spell checker (streetsidesoftware.code-spell-checker)
indent-rainbow (oderwat.indent-rainbow)
jinja2 (wholroyd.jinja)
pretty formatter (mblode.pretty-formatter)
python-poetry (zeshuaro.vscode-python-poetry)
trailing spaces (shardulm94.trailing-spaces)
markdownlint (DavidAnson.vscode-markdownlint)
even better TOML (tamasfe.even-better-toml)
```

## Step 3: Configuring Your CLI

### Install Zsh

``` bash
sudo apt update
sudo apt install zsh
```

### Install Oh-My-Zsh

``` bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### Zsh Plugins

``` bash
# Zsh Completions
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions

# Zsh Auto Suggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### Install Powerlevel 10k

``` bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Add this to the end of `.zshrc`

``` bash
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(z vscode git emoji encode64 history sudo web-search jsontools zsh-completions zsh-autosuggestions)
```

Some fonts maybe required for powerlevel. Download the four fonts from this website and install (https://github.com/romkatv/powerlevel10k#manual-font-installation).

You will then need to add the font to VSCode. To do this you need to open your user settings JSON, this can be done from the command pallet.

``` json
{
    "editor.fontFamily": "MesloLGS NF, Consolas, 'Courier New', monospace"
}
```

### Set Defaul Shell

``` bash
chsh -s $(which zsh)
```

## Step 4: Python

Installing poetry:

``` bash
curl -sSL https://install.python-poetry.org | python3 -
```
