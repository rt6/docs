# VIM, Plugins, Vundle

### 1. Install VIM Plugins using Vundle Plugin Manager

```bash
# first backup your .vimrc and .vim directory
$ mv ~/.vimrc ~/.vimrc_old
$ mv ~/.vim ~/.vim_old

# install git (if you don't already have it)
$ sudo apt install git

# download Vundle
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

add the following to the ~/.vimrc file
```viml
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

set cursorline
set number
set tabstop=8 softtabstop=0 expandtab shiftwidth=4 smarttab
set autoindent
autocmd VimEnter * NERDTree
```

Don't close vim and execute these commands
```
: source %
: PluginInstall
```

Note: To enable Solarize color in Ubuntu Tmux, add the following 2 lines to `.bashrc` and `.tmux.conf`

~/.bashrc:
```
alias tmux="TERM=screen-256color-bce tmux"
```

Now exit and run `$ source ~/.bashrc`

~/.tmux.conf:
```
set -g default-terminal "xterm-256color"`
```

Now everything should work ! :) Nerdtree (and other plugins) have been installed and will automatically start next time you open Vim

### 2. Useful NerdTree commands
`enter` open file

`I` show/hide hidden files

`Ctrl w,  w ` switch between explorer and file

`T` open file in new background tab

`t` open file and switch to tab

`gT` or `gt` switch between tabs
