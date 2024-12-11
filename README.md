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

