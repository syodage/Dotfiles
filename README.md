# Configure a new Workspace

This (bare)repo contains all the important config files and instrunctions to setup a new workspace.

## Terminal 

1. Install Alacritty Terminal

```sh
sudo apt update && sudo apt upgrade
sudo apt-get install alacritty
alacritty --version
```

1. Install [zsh]()

```zsh
sudo apt install zsh
zsh --version
# make zsh the default shell
chsh -s $(which zsh)
```

1. Install [Oh-my-zsh](https://ohmyz.sh/#install)

```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Github Repo

1. Create a new ssh-key([github tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)) and add it to the github.

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## Track configs 

Atlassian has a really good [tutorial](https://www.atlassian.com/git/tutorials/dotfiles) explaning the whole workflow. Following are extract of that tutorial.

### Setup bare repository

1. Initiate the bare repository `git init --bare $HOME/.cfg`

1. Add a new function to wrap bare git command

```zsh
function config {
   /usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME $@
}
```

1. Update config to don't show untrack files. ` config config --local status.showUntrackedFiles no`

### Setup existing bare repository

1. First clone the repository to the local directory. 

```zsh
git clone --bare https://bitbucket.org/durdn/cfg.git $HOME/.cfg
```

1. Add config function to .zshrc

```zsh
function config {
   /usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME $@
}
```

1. Checkout the repo and update configs to not to show untracked files.

```zsh
config checkout
config config status.showUntrackedFiles no 
```
## Neovim

1. Download Neovim binary from [here](https://neovim.io/) 

1. Extract binary and add it to $PAtH env variable.

```sh
# Create `Tools` directory if not exist
mkdir -p ~/Tools
cd Downloads
tar -zxf nvim-linux64.tar.gz
# Append version to the directory
mv nvim-linux64 ~/Tools/nvim-linux64_v094
echo "export PATH=$HOME/Tools/nvim-linux64_v094/bin:$PATH" >> ~/.zshrc
exec zsh
```

1. Follow [install instrunctions](https://docs.astronvim.com/#%EF%B8%8F-installation) to install [Astronvim]() distro.

```sh
# back up existing nvim config if any
mv ~/.config/nvim ~/.config/nvim.bak
# clean nvim folders
mv ~/.local/share/nvim ~/.local/share/nvim.bak
mv ~/.local/state/nvim ~/.local/state/nvim.bak
mv ~/.cache/nvim ~/.cache/nvim.bak
# Clone Astronvim
git clone --depth 1 https://github.com/AstroNvim/AstroNvim ~/.config/nvim
nvim
```

1. If neovim is available alias `vim` to `nvim` 

```sh
if type nvim > /dev/null 2>&1; then
    alias vim=nvim
fi

export EDITOR=nvim
export VISUAL=nvim
```

## Install i3wm

Run `sudo apt-get insatall i3` and logout and log back to i3

