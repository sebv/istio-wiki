## Releases before 0.5:

- Make sure the images used are not the `_debug` images (use `istioctl kube-inject --debug=false`)

- Check the ingress images

- Remove `-v 2`

You can do both of those steps like [this script](https://github.com/istio/istio/blob/a957c58b0ef7f745643b40f4f156dac7bcfc43d2/tools/setup_perf_cluster.sh#L112)

## Starting in 0.5:

The default are non debug. :tada:

## General:

- Setup multiple pilot, mixers
- Tweak/tune the istio config map to only use what you need

See also the [Performance Testing guide](https://github.com/istio/istio/tree/master/tools#istio-load-testing-user-guide) and the scripts in https://github.com/istio/istio/tree/master/tools