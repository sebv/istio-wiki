Current hot topics for the Policies and Telemetry working group

* Out-of-process (gRPC) Adapters

  We want to enable Mixer integration without requiring custom builds of Mixer to enable new adapter functionality. This topic is concerned with how Mixer will integrate with out-of-process adapters, how such adapters will be deployed and managed, and how configuration of the adapters will be handled. Additional sub-topics include debugging and testing.

* Configuration scheme

  Mixer currently uses multiple distinct Custom Resource Definitions (CRDs) to capture the individual configuration for adapters and instance types. This proliferation of configuration resources causes a number of issues, not least of which is configuration burden. We want to simplify the Mixer configuration story, consolidating on three/four higher-level CRDs that can model the same information.

* Client-side policy enforcement and telemetry collection

  This work is to enable client-side Mixer integration for Istio. To date, Istio's Mixer integration has been server-side (service receiving traffic makes calls out to Mixer for `Check()` and `Report()`). This has meant that Istio cannot "see" client-side errors (including in cases like fault-injection) and cannot handle policy enforcement on the client-side (in situations such as Ingress when this might be appropriate).

* Source Attribution

  The working group is attempting to define how to properly identify the source of traffic via attributes. There is concern that `source.service` is not appropriate for workloads that implement multiple services and for workloads that do not participate in any services. Further, there is concern over the integrity of any `source.*` attribute that is not verified via mTLS handshake.

* Mixer Direct API

  


