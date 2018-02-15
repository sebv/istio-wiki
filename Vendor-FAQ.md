Istio uses vendored dependencies through a submodule. This avoids having huge unrelated commit mixed with our actual work while having the benefits of hermetic reproducible builds and fast dependency download.

## How do I get setup
One time / first time setup

### Existing clone/fork:

If you have a pre Feb 15 2018 fork or clone:

```
rm -rf ./vendor/
make init
```

### New repo
```
git clone --recurse-submodules https://github.com/istio/istio.git
```

or even better (as it will place the source tree in the right location for go):
```
go get istio.io/istio
```

## How do I stay in sync
```
make pull
```

or manually
```
git submodule sync && git submodule update
```

## How do I add / change a dependency

Edit the [Gopkg.toml](https://github.com/istio/istio/blob/master/Gopkg.toml).

Run `dep ensure`

`cd vendor/` and `git status` / check `git diff`, make a PR for the changes

Once approved/merged (or on a branch of the vendor repo): submit your PR once the submodule change doesn't show `-dirty`


## How do we auto update dependencies

A periodic job can run `dep ensure` and commit a vendor submodule PR first and if approved and passing the test move the `vendor/` in istio/istio
