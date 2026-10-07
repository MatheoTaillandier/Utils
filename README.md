# Utils repository
## uv
uv is a tool for managing Python dependencies and virtual environments. It allows you to easily create and manage virtual environments, as well as install and manage dependencies for your projects. Using the following commands, there is no need to create a venv manually or to manage the dependencies in a requirements.txt file. uv will handle all of that for you.

To use uv, install it and run the following command in the repository :
```
uv init (--python $version$)
```

To install dependencies, run the following command in the repository :
```
uv sync
```

To add a dependency, run the following command in the repository :
```
uv add $dependency$
```

To remove a dependency, run the following command in the repository :
```
uv remove $dependency$
```

To run a command in the virtual environment, run the following command in the repository :
```
uv run $command$
```

## Pre-commit
To use pre-commit hooks, install pre-commit and run the following command in the repository :
```
pre-commit install
```

pre-commit hooks are defined in the .pre-commit-config.yaml file. You can add or remove hooks as needed. To run the hooks manually, run the following command in the repository :
### Hooks used
- **ruff** : a linter and formatter for Python code (uses the --fix option to automatically fix issues)
- **detect-secrets** : a tool for detecting secrets in code to prevent them from being committed to version control

### Github actions
For github actions that implement the same checks as the pre-commits, view the actions for this repo

# Utils Ubuntu
## Terminal
### For shortening and un-shortening the path in terminal :

Add to .bash_aliases :
```
# START of custom commands

# Save current prompt and shorten it
shortpath() {
    export ORIGINAL_PS1="$PS1"   # store current prompt
    export PS1="\W \$ "          # shorten to current directory only
}

# Restore the original prompt
longpath() {
    export PS1="$ORIGINAL_PS1"   # restore prompt
}

# Checkout PR
gpr() {
    if [ -z "$1" ]; then
        echo "Cleaning up local PR branches..."
        local current_branch
        current_branch="$(git branch --show-current)"
    
        # Switch to main if currently on a PR branch
        if [[ "$current_branch" =~ ^pr/[0-9]+$ ]]; then
            echo "Currently on PR branch '$current_branch'. Switching to main..."
            git checkout main || return 1
        fi
    
        # Delete all local PR branches
        git branch | grep -E '^[* ]*pr/[0-9]+$' | xargs -r git branch -D
    else
        local remote="${2:-origin}"
        git fetch "$remote" "pull/$1/head:pr/$1" && git checkout "pr/$1"
    fi
}

# ==============================================================================
# NAVIGATION & DIRECTORY LISTING
# ==============================================================================
# Easier navigation
alias ..="cd .."
alias ...="cd ../.."
alias ....="cd ../../.."
alias .....="cd ../../../.."
alias ~="cd ~"
alias bd="cd -" # Quick jump back to the previous directory

# Modern/detailed ls alternatives
alias ls='ls --color=auto'
alias ll='ls -alF'           # Long format with hidden files & indicators
alias la='ls -A'             # Show almost all (includes hidden, excludes . and ..)
alias l='ls -CF'
alias lx='ls -lXB'           # Sort by extension
alias lk='ls -lS'           # Sort by size, largest first
alias lt='ls -lt'           # Sort by date, newest first

# ==============================================================================
# SAFETY & DEFAULTS
# ==============================================================================
# Confirmation before destructive actions
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups  # no duplicate history entries

# Prevent accidental overwrites when making directories
alias mkdir='mkdir -pv'      # Verbose + create parent directories as needed
mkcd() { mkdir -p "$1" && cd "$1"; }     # make dir and cd into it in one step

# ==============================================================================
# SYSTEM & RESOURCE MONITORING
# ==============================================================================
# Disk and Memory usage (human-readable format)
alias df='df -h'
alias du='du -h'
alias free='free -m'
alias pk='pkill -f'

# Quick check on top processes
alias topcpu='ps auxf | sort -nr -k 3 | head -10'
alias topmem='ps auxf | sort -nr -k 4 | head -10'

# Easily check open ports
alias ports='ss -tulpn'
portuse() { lsof -i ":$1"; }

# ==============================================================================
# FIND & SEARCH
# ==============================================================================
alias grep='grep --color=auto'
ff() { find . -iname "*$1*"; }                                  # find file by (partial) name
fcd() { cd "$(find . -type d -iname "*$1*" | head -1)"; }       # find dir by name and cd into it
fe() { nano "$(find . -type f -iname "*$1*" | head -1)"; }      # find file by name and open it
alias biggest='du -ah . | sort -rh | head -50'                  # biggest files/dirs in current folder

# ==============================================================================
# GIT CONVENIENCE
# ==============================================================================
alias g='git'
alias gs='git status -s'
alias ga='git add'
alias gaa='git add --all'
alias gc='git commit -m'
alias gco='git checkout'
alias gb='git branch'
alias gl='git log --oneline --graph --decorate'
alias gp='git push'
alias gpf='git push --force-with-lease'
alias gpl='git pull'
alias gd='git diff'
gdbase() { git diff "$(git merge-base HEAD main)"; }
alias gdm='git diff main'
alias gss='git stash'
alias gsp='git stash pop'
alias gcm='git checkout main'
alias grb='git rebase'
alias gcp='git cherry-pick'
alias gundo='git reset --soft HEAD~1'

# ==============================================================================
# NETWORK & IP UTILITIES
# ==============================================================================
# Get local and public IP addresses
alias myip="curl -s https://ipinfo.io/ip"
alias localip="hostname -I | awk '{print \$1}'"

# Ping shortcut with reasonable limits
alias fastping='ping -c 5 1.1.1.1'

# ==============================================================================
# ROS2
# ==============================================================================
# Source a specific ROS2 version
alias RosLyrical='source /opt/ros/lyrical/setup.bash'
alias cbuild='colcon build --symlink-install'
alias csource='source install/setup.bash'

# ==============================================================================
# DOCKER
# ==============================================================================
alias d='docker'
alias dc='docker compose'
alias dps='docker ps'
alias dpsa='docker ps -a'
alias dimg='docker images'
alias dstop='docker ps -q | xargs -r docker stop'
alias drm='docker ps -aq | xargs -r docker rm'
alias drmi='docker images -q | xargs -r docker rmi'
alias dlog='docker logs -f'
dsh() { docker exec -it "$1" "${2:-bash}"; }                 # shell into container: dsh <name> [shell]
alias dprune='docker system prune -af'                       # reclaim disk space (careful: destructive)

# ==============================================================================
# PYTHON / VENV
# ==============================================================================
alias venv='uv venv && source .venv/bin/activate'
alias activate='source .venv/bin/activate'
alias rmvenv='deactivate 2>/dev/null; rm -rf .venv'

# ==============================================================================
# MISCELLANEOUS & UTILITIES
# ==============================================================================
alias please='sudo $(fc -ln -1)'           # rerun last command with sudo

# Edit this file quickly
alias aliases='nano ~/.bash_aliases'

# Reload bash configuration quickly
alias reload='source ~/.bashrc'

# Quick text editor shortcut
alias nano='nano -l'          # Always show line numbers in nano

# Search history easily
alias h='history'
alias hg='history | grep'

# Clear screen shortcut
alias c='clear'
alias cls='clear'

alias path='echo -e ${PATH//:/\\n}'      # print $PATH, one entry per line
alias now='date +"%Y-%m-%d %H:%M:%S"'
extract() {                              # universal archive extractor
    case "$1" in
        *.tar.gz|*.tgz) tar xzf "$1" ;;
        *.tar.bz2) tar xjf "$1" ;;
        *.tar) tar xf "$1" ;;
        *.zip) unzip "$1" ;;
        *.gz) gunzip "$1" ;;
        *) echo "Unsupported format: $1" ;;
    esac
}

# END of custom commands
```

### Commands : 
`shortpath` to shorten the path \
`longpath` to make it long again \
`gitpr`checkout PR from a repo \
`Ros$Version$` to source the setup.bash for this version and use system python

## ROS
### For ROS over wifi : 
- set $ROS_LOCALHOST_ONLY = 0
- Setup cyclonedds and its xml file
Add to .bashrc :
```
export ROS_DOMAIN_ID = $$ # $$ (0-101) needs to be the same on all the machines
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
export CYCLONEDDS_URI=file:///home/YOUR_USER/cyclonedds.xml
```


# Utils Windows
## SSH
To add ssh keys for multiple github accounts : view the template `ssh_config`
To clone using specific ssh key : 
```
git clone git@$HOST$:MatheoTaillandier/Utils.git
```
