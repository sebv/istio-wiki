# Daily build information

> Those daily builds aren't meant for general consumption

The dailies are published on
http://gcsweb.istio.io/gcs/istio-prerelease/daily-build/

## Notes:
* You want to use the TESTONLY tar as they are the one with referencing images that exist (until [#2904](https://github.com/istio/istio/issues/2904) is fixed)
* You may encounter issue with the page not loading (https://github.com/istio/istio/issues/1885 and https://github.com/istio/test-infra/issues/675): use curl or a different browser, with chrome check [`chrome://net-internals/#hsts`](chrome://net-internals/#hsts) and delete the entry for istio.io

