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
# Utils Ubuntu
## Terminal
### For shortening and un-shortening the path in terminal :

Add to .bashrc :
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

# END of custom commands
```

### For sourcing a specific ROS version :
Add to .bashrc :

```
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

Add to .bash_aliases : 
```
alias Ros$Version$='source /opt/ros/$version$/setup.bash && pyenv shell system'
```

### Commands : 
`shortpath` to shorten the path \
`longpath` to make it long again \
`Ros$Version$` to source the setup.bash for this version and use system python

# Utils Windows
## SSH
To add ssh keys for multiple github accounts : view the template `ssh_config`
To clone using specific ssh key : 
```
git clone git@$HOST$:MatheoTaillandier/Utils.git
```
