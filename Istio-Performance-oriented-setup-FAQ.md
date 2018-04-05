## Releases before 0.5:

- Make sure the images used are not the `_debug` images (use `istioctl kube-inject --debug=false`)

- Check the ingress image

- Remove `-v 2`

You can do both of those steps like [this script](https://github.com/istio/istio/blob/a957c58b0ef7f745643b40f4f156dac7bcfc43d2/tools/setup_perf_cluster.sh#L112)

## Starting in 0.5:

The default images and config are now the non debug ones. :tada:

To switch back debug logging for mixer:
```
$ kubectl edit deployment -n istio-system istio-mixer
# Add to args list:
        - --log_output_level=debug
```

## General:

- Setup multiple pilot, mixers
- Tweak/tune the istio config map to only use what you need

### [Automatic proxy injection](https://istio.io/docs/setup/kubernetes/sidecar-injection.html#automatic-sidecar-injection)

Automatic proxy injection is implemented as a webhook using Kubernetes MutatingWebhook. Its stateless, depending only on the injection template and mesh configuration configmaps as well as the to-be-injected pod object. As such, it can be easily horizontally scaled, either manually via the [deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment) object, or automatically via a [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/).

It only takes an average 1.5us for the webhook itself to inject the sidecar proxy into a newly created pod per [micro benchmark](https://github.com/istio/istio/pull/3189/files#diff-3fb712a20331a79c4b1c1eda38704a76R515). Total injection time will be obviously much higher when accounting for network latency and api-server processing time (TBD/measure).

## Perf analysis tools

To debug/install [perf(1)](http://www.brendangregg.com/perf.html) on GKE nodes for instance:

https://cloud.google.com/container-optimized-os/docs/how-to/toolbox#installing_and_running_tools_from_toolbox

## See also

See also the [Performance Testing guide](https://github.com/istio/istio/tree/master/tools#istio-load-testing-user-guide) and the scripts in https://github.com/istio/istio/tree/master/tools

The [Perf&Scalability WG](https://github.com/istio/community/blob/master/WORKING-GROUPS.md#performance-and-scalability), and the https://ibmcloud-perf.istio.io/regpatrol/ and https://fortio.istio.io/ results it produces.