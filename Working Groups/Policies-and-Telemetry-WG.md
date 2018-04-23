## Weekly Meeting
* Zoom Meeting Link: [https://istio.zoom.us/j/576917606](https://istio.zoom.us/j/576917606)
* Agenda and Notes: [https://bit.ly/2JgmDes](https://bit.ly/2JgmDes)
* YouTube playlist: [https://www.youtube.com/watch?v=z-z6MqIalN4&list=PL7wB27eZmdffF-9nyaw01Ni_0GOWBzaF4](https://www.youtube.com/watch?v=z-z6MqIalN4&list=PL7wB27eZmdffF-9nyaw01Ni_0GOWBzaF4) 

## On-going discussions:
1. RE: Client-side telemetry
   
   **Open issue**: Should both client- and server-side `Report()`s be enabled by default (when available)? And who "owns" client-side metrics (should service owners be able to see the data of their clients)?

   Initial proposal is to have both on by default; allow operator customization.

1. RE: gRPC adapters

   **Open issue**: How should gRPC adapters be namespaced (if at all)?

   A doc is needed that spells out full implications (Mandar/Sunny to provide).

1. RE: Service identity
   
   **Open issue**: How are source workloads identified within Istio? What design pattern and best-practices should we document / encourage?

   This discussion is going on both in WG meetings and on the mailing-list.

## Recent Design Decisions


***

Learn more about the [Policies & Telemetry working group](https://github.com/istio/community/blob/master/WORKING-GROUPS.md#policies-and-telemetry).
