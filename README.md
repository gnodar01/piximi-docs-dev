## First Time Setup

Ignore this if cloning. This is just the series of steps in first setting up this repo's submodule.

```sh
git submodule add -b main git@github.com:piximi/documentation.git documentation/
git submodule update --init --recursive
git add .gitmodules documentation/
git commit -m "Add submodule for documentation repository
```

## Setup

Clone the directory and setup submodules:

```bash
git clone git@github.com:gnodar01/piximi-docs-dev.git
git submodule init
git submodule update --remote
```

[Install pixi](https://pixi.sh/latest/#installation)

```bash
curl -fsSL https://pixi.sh/install.sh | bash
```

Install the project dependencies:

```bash
pixi install --all
```

Run build:

```bash
pixi run build
```

View the build in browser:

```bash
pixi run view
```

## Development

If there are changes in the `main` branch of the submodule, pull the updates:

```sh
git submodule update --remote documentation/
```

Check the status of a submodule:

```sh
git submodule status
```

Work in the submodule:

```sh
cd documentation

# normal development
# e.g.
git switch dev-branch
# ...modify files
git add -A
git commit -m "change such and such"
git push

cd ..
git add documentation/
git commit -m "Update submodule reference"
```

NOTE: A `post-checkout` git hook has been added. When doing `git switch <branch_name>` in the dev repo, it will mirror a checkout of the same branch name in the `documentation/` submodule.

This is the `post-checkout` script:

```sh
#!/bin/bash

# Get the current branch of the parent repository
current_branch=$(git symbolic-ref --short HEAD)

# Navigate to the submodule directory and switch to the same branch
submodule_path="documentation" # Change this to your submodule's path
if [ -d "$submodule_path" ]; then
    cd "$submodule_path"
    git fetch origin "$current_branch"
    if git rev-parse --verify "$current_branch" >/dev/null 2>&1; then
        git switch "$current_branch"
    else
        git switch -c "$current_branch" origin/"$current_branch"
    fi
    cd ..
fi
```

