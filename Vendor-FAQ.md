Istio uses vendored dependencies through a submodule. This avoids having large unrelated commits mixed with our actual work while having the benefits of hermetic reproducible builds, tracked changes and fast dependencies download.

## How do I get setup?
One time / first time setup

### Existing clone/fork:

If you have a pre Feb 15 2018 fork or clone:

```
rm -rf ./vendor/ # only do that if vendor/ is a plain directory without a .git
make init
( cd vendor && git checkout master && git pull )
```

### New repo
```
git clone --recurse-submodules https://github.com/istio/istio.git
cd istio/vendor && git checkout master && git pull
```

or even better (as it will place the source tree in the right location for go):
```
go get istio.io/istio
```

## How do I stay in sync?

1 time setup that helps if you will be changing the dependencies:
```
cd vendor && git checkout master && git pull
```
then regularly
```
make pull
```

or manually, when you notice that [Gopkg.lock](https://github.com/istio/istio/blob/master/Gopkg.lock) changed:

```
git submodule sync && git submodule update
```

## How do I check my setup is ok vendor wise?

```
# in ~/go/src/istio.io/istio
cd vendor; git status; git remote -v
```
should output
```
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
origin	https://github.com/istio/vendor-istio.git (fetch)
origin	https://github.com/istio/vendor-istio.git (push)
```

If you get something else, see setup above

## How big is vendor, how much of a download?
```
# during clone, submodule download is ~8Mb
Receiving objects: 100% (4280/4280), 7.96 MiB | 6.93 MiB/s, done.
# size once expanded
$ du -hs vendor/
 54M	vendor/
# it used to be 407Mb before
```
This is thanks to the [pruning](https://github.com/istio/istio/pull/3348/files#diff-836546cc53507f6b2d581088903b1785R39) setup in go dep.

## How do I add / change a dependency?

Edit the [Gopkg.toml](https://github.com/istio/istio/blob/master/Gopkg.toml).

Run `dep ensure`

`cd vendor/` and `git status` / check `git diff`, make a PR for the changes

Once approved/merged (or on a branch of the vendor repo): submit your PR once the submodule change doesn't show `-dirty`


## Should I merge changes in `vendor/`?

No, If you see in your `git status`
```
	modified:   vendor (untracked content)
```
Do not add this to your PR. Unlike you explicitly wanted to make dependency changes, see next question:

## How do we auto update dependencies?

A periodic job can run `dep ensure` and commit a vendor submodule PR first and if approved and passing the test move the `vendor/` in istio/istio
