Istio has many moving parts. 
When a problem is reported by a customer, it is useful to know the full state of system.

## Option A: Run `bin/dump_kubernetes.sh`

```sh
curl https://raw.githubusercontent.com/Tahler/istio/ba69dff344d5a4a68c91b06b7bb5f268bf6b05e7/bin/dump_kubernetes.sh | sh -s -- -z
```

Or run the script locally from the root of this repository:

```sh
bin/dump_kubernetes.sh -z
```

Then send the outputted "istio-dump.tar.gz" along with your reported problem.

## Option B: Manual collection

If you are unable to follow option A and run the script, manually gather the following info:

 * State of all pods running in the system.  (`kubectl get pods -o yaml --all-namespaces`)
 * services
 * Deployments
 * Endpoints

`kubectl get pods,services,deployments,endpoints --all-namespaces -o yaml > k8s_resources.yaml`

 * Names of secrets in `istio-system`:  `kubectl --namespace istio-system get secrets`
 * Config maps in `istio-system`: `kubectl --namespace istio-system get cm -o yaml`
 * Logs from all istio-components and istio-sidecars. This should include both current and previous logs.
   * `foreach kubectl logs POD_name -c istio-proxy`
 * Mixer Logs:
   * `kubectl logs -n istio-system -listio=mixer -c mixer`
   * `kubectl logs -n istio-system -listio=policy -c mixer`
   * `kubectl logs -n istio-system -listio=telemetry -c mixer`
 * Pilot Logs:
   * `kubectl logs -n istio-system -listio=pilot -c discovery`
   * `kubectl logs -n istio-system -listio=pilot -c istio-proxy`

* All Istio configuration artifacts.
  * `kubectl get $(kubectl get crd  --no-headers | awk '{printf "%s,",$1}END{printf "attributemanifests.config.istio.io\n"}') --all-namespaces`

 ## TODO Turning on debug on Istio components

