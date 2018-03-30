# Daily build information

> Those daily builds aren't meant for general consumption

The dailies are published on
https://gcsweb.istio.io/gcs/istio-prerelease/daily-build/


Notes:
- The file name's timestamp is in UTC
- gcsweb also shows time in UTC

Installing the builds can be similar to installing the releases.  I install like this:

```
DAILY=0.7.0-pre20180325-09-15  # or whichever version you wish
curl -L https://git.io/getLatestIstio \
   | sed 's/github.com\/istio\/istio\/releases\/download/storage.googleapis.com\/istio-prerelease\/daily-build/'\
   | ISTIO_VERSION=$DAILY sh -
cd istio-$DAILY
```
