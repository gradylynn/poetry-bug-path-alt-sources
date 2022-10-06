I think that that this repo demonstrates a bug in the way that poetry installs
path dependencies that use non-pypi sources.

It appears that poetry does not use the non-pypi source defined in `./my_package/pyproject.toml` to install the dependency defined in `./my_package/pyproject.toml`.
Instead, it uses sources from `./pyproject.toml`, which can be demonstrated by uncommenting the source in `./pyproject.toml`.

Expected Behavior:
```
> poetry install          
Updating dependencies
Resolving dependencies... (0.1s)

Writing lock file

Package operations: 2 installs, 0 updates, 0 removals

  • Installing roslz4 (1.14.3.post2)
  • Installing my-package (0.0.1 /Users/glynn/Desktop/poetry-bug/my_package)
```

Actual Behavior:
```
> poetry install
Updating dependencies
Resolving dependencies... (0.0s)

Because my-package (0.0.1) @ file:///path/to/my_package depends on roslz4 (^1.14.0) which doesn't exist, my-package is forbidden.
So, because the-best-codebase-ever depends on my_package (0.0.1) @ my_package, version solving failed.
```
