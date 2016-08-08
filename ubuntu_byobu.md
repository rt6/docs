# BYOBU
Byobu is a wrapper for Tmux and Screen.  It has a colorful status bar with useful statistics (cpu usage, ip number, memory usage, etc) and some fancy shortcuts.

### Installation

```sh 
# install
$ sudo apt install byobu

# check version
$ byobu --version

# auto start byobu upon connection
$ byobu-enable

# show colorful prompt
$ byobu-enable-prompt

# reload bashrc
. ~/.bashrc

# remember to close all tmux sessions and reconnect to server to see byobu prompts

```

### Note: 

`Ctrl a` is command shortcut instead of `ctrl b` as used in tmux
 
 `F9` to choose status bar notifications (cpu temperature, memory, ip number, host name etc).  You can also change the command shortcut (aka escape sequence) to `ctrl b` 
 
 
