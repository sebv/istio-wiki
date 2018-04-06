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

## Troubleshooting

### No Daily Release Today
Check https://prow.istio.io/?author=istio-release-robot. Any release qualification test failure can block the daily release. Please file an issue if the error looks new (i.e. not currently tracked by any issue).
