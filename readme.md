🐧 Default .bashrc for WSL (Windows Subsystem for Linux)
Welcome to the default .bashrc configuration for Windows Subsystem for Linux (WSL), tailored for Ubuntu-based distributions. This file customizes your interactive non-login shell with aliases, colorful prompts, history settings, and more to enhance your terminal experience.
🌟 Star this repo if you find it useful, and feel free to contribute or suggest improvements!

📍 Overview
The .bashrc file is executed by bash for interactive non-login shells in WSL. It configures:

🖌️ Prompt customization with colors and chroot support
📜 Command history settings to avoid duplicates
🔧 Aliases for common commands like ls and grep
🔔 Desktop notifications for long-running commands
🛠️ Tab completion and external tool integration


📁 File Location
The .bashrc file is located at:
~/.bashrc


📜 Default .bashrc Content
Below is the complete default .bashrc file for WSL (Ubuntu-based distributions).
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
        color_prompt=yes
    else
        color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi


🔍 Key Features Explained
🧠 Shell Behavior

Interactive Shell Check: Exits early for non-interactive shells to prevent unnecessary processing.
History Management: 
HISTCONTROL=ignoreboth avoids duplicate commands and space-prefixed entries in history.
shopt -s histappend appends to .bash_history instead of overwriting.
HISTSIZE=1000 and HISTFILESIZE=2000 set generous history limits.



🎨 Prompt Customization

Colored Prompt: Enabled for xterm-color or *-256color terminals with a green username and blue working directory.
Force Colors: Uncomment force_color_prompt=yes to enable colors on compatible terminals:force_color_prompt=yes


Chroot Support: Displays the chroot name (if applicable) in the prompt.

🧾 Useful Aliases

ls aliases: ll (ls -alF), la (ls -A), l (ls -CF) for quick directory listing.
grep aliases: Colorized output for grep, fgrep, and egrep.
alert: Sends desktop notifications for long-running commands (e.g., sleep 10; alert).

📦 External Files & Tools

Custom Aliases: Loads ~/.bash_aliases for user-specific aliases.
Tab Completion: Enables bash-completion for smarter tab completion.
Lesspipe: Enhances less for viewing non-text files.
Dircolors: Adds color support to ls output.


💻 How to Use in WSL

Backup Your Existing .bashrc:
cp ~/.bashrc ~/.bashrc.backup


Replace with This .bashrc:
curl -o ~/.bashrc https://raw.githubusercontent.com/<your-username>/<your-repo>/main/.bashrc


Reload the Shell:
source ~/.bashrc




⚙️ Customization Tips

Add Custom Aliases: Create a ~/.bash_aliases file for your own aliases:
echo "alias gs='git status'" >> ~/.bash_aliases


Enable Globstar: Uncomment shopt -s globstar for recursive globbing with **:
shopt -s globstar


Desktop Notifications: Use with WSLg, VcXsrv, or X410 for alert notifications to work.
