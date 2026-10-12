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

For useful aliases, see the the `.bash_aliases` file.
To source this file inside your bash, add the following to your bashrc : 
```
if [ -f <PATH_TO_UTILS_REPO>/.bash_aliases ]; then
    . <PATH_TO_UTILS_REPO>/.bash_aliases
fi

```

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
