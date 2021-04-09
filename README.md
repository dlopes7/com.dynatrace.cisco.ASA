# <repo-name>
<repo-description>

## Usage
For now go for [dev](#dev)

## Dev

### Prerequisites
- [nix](https://nixos.org/nix/manual/#chap-installation)
- `direnv` (`nix-env -iA nixpkgs.direnv`)
- [configured direnv shell hook ](https://direnv.net/docs/hook.html)
- some form of `make` (`nix-env -iA nixpkgs.gnumake`)

Hint: if something doesn't work because of missing package please add the package to `default.nix` instead of installing on your computer. Why solve the problem for one if you can solve the problem for all? ;)

#### Other
- ssh access to [snmp datasource repository](https://bitbucket.lab.dynatrace.org/projects/ONE/repos/datasource-go/browse/snmp)

### One-time setup
```
make init
```

### Everything
```
make help
```

### Bumping datasource version
You'll need to specify full commit hash, "84e18789e7b46b8d19acccbeb0d6ab543742d72b" will work and "84e18789e" **won't**
