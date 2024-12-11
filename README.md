First time setup:

```sh
git submodule add -b main git@github.com:piximi/documentation.git documentation/
git submodule update --init --recursive
git add .gitmodules documentation/
git commit -m "Add submodule for documentation repository
```

