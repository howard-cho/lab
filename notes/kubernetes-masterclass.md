# Required packages

## `brew`
- `tmux`
- `vim` or `nvim`
- `bash-completion` (for Linux/WSL)
- `kubectl`
- `k9s`

## `.bashrc`

Set up `.bashrc` for `kubectl` completion by adding the following:

    alias k='kubectl'
    source /etc/bash_completion # not needed on macos
    source <(kubectl completion bash)
    complete -o default -F __start_kubectl k

## `.zshrc`

Set up `.zshrc` for `kubectl` completion by adding the following:

    # kubectl
    autoload -Uz compinit
    compinit

    alias k='kubectl'

    source /etc/bash_completion
    source <(kubectl completion zsh)
    # complete -o default -F __start_kubectl k

    alias kgp='kubectl get pods'
    alias kc='kubectx'
    alias kn='kubens'

    alias kcs='kubectl config use-context admin@homelab-staging'
    alias kcp='kubectl config use-context admin@homelab-production'

## `.vimrc`

This is a basic `.vimrc` for YAML editing:

Ensure Vim uses filetype plugins

    filetype plugin on

Enable indentation

    filetype indent on

Set the default indentation to 2 spaces for all files

    set tabstop=2
    set softtabstop=2
    set shiftwidth=2
    set expandtab

Highlight trailing whitespace in all files

    autocmd BufRead,BufNewFile * match Error /\s\+$/

Enable auto-indentation

    set autoindent

Turn on syntax highlighting

    syntax on

Set backspace so it acts more intuitively

    set backspace=indent,eol,start

## `tmux` config

Edit/create `~/.tmux.conf`

    set-option -g history-limit 25000
    set -g mouse on

    # for neovim
    set -sg escape-time 10
    set-option -g focus-events on

    # vi for copy mode
    setw -g mode-keys vi

    # status bar
    set -g status-right "#(pomo)"
    set -g status-style "fg=#665c54"
    set -g status-left-style "fg=#928374"
    set -g status-bg default
    set -g status-position top
    set -g status-interval 1
    set -g status-left ""

    # disable status
    # set -g status off
    # set -g status on

    # count the panes from 1
    set -g base-index 1
    setw -g pane-base-index 1

    # reload configuration
    bind-key -r r source-file ~/.tmux.conf

    # term colors, these are the correct ones according to neovim checkhealth
    set-option -g default-terminal "screen-256color"