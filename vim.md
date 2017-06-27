# VIM, Plugins, Vundle

### 1. Install VIM Plugins using Vundle Plugin Manager

```bash
# first backup your .vimrc and .vim directory
$ mv ~/.vimrc ~/.vimrc_old
$ mv ~/.vim ~/.vim_old

# install vim
$ sudo apt install vim

# install git (if you don't already have it)
$ sudo apt install git

# download Vundle
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

# download .vimrc
$ cd ~
$ wget -O ~/.vimrc https://raw.githubusercontent.com/rt6/dotfiles/master/.vimrc 

# open vim (ignore the error messages about missing plugins)
$ vi

# install plugins using vim
: source %
: PluginInstall

```

Note: To enable Solarize color in Ubuntu Tmux and Byobu, add the following 2 lines to `.bashrc` and `.tmux.conf`

~/.bashrc:
```
(Ubuntu)
export TERM=screen-256color 

or 

alias tmux="TERM=screen-256color-bce tmux"
```

Now exit and run `$ source ~/.bashrc`

~/.tmux.conf (not needed for byobu):
```
(Mac)
set -g default-terminal "xterm-256color"

(Ubuntu VIM)
set -g default-terminal "screen-256color"
```




Now everything should work ! :) Nerdtree (and other plugins) have been installed and will automatically start next time you open Vim

### 2. Useful NerdTree commands
`enter` open file

`I` show/hide hidden files

`ctrl ww ` switch between explorer and file

`T` open file in new background tab

`t` open file and switch to tab

`gT` or `gt` switch between tabs

`ma` create new file or directory

`mm` rename file or directory

`md` delete name or directory

`mc` copy file or directory

`\` find file like VIM

`go` preview file

`gi` preview file in horizontal split

`ctrl d` scroll down tree

`ctrl u` scroll up tree

`ctrl b` switch window

`ctrl c` new window


### 2. VIM NERD Commenter commands

`\cc` comment line

`\c <spacebar>` uncomment line

`\cm` block comment

`\cs` pretty block comment


