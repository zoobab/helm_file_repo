# Helm plugin for file://

This plugin adds support for local repositories to helm with the `file://` instead of `http://` or `https://`.

Example:
```
$ helm plugin add https://github.com/zoobab/helm_file_repo
Installed plugin: file
# Alternatively, you could also add it locally with: 
# $ git clone https://github.com/zoobab/helm_file_repo && helm plugin add ./helm_file_repo
$ helm create chartexample
Creating chartexample
$ cd chartexample
$ helm package .
Successfully packaged chart and saved it to: /tmp/workdir/chartexample/chartexample-0.1.0.tgz
$ cd ..
$ mkdir helm_cache
$ cp -v ./chartexample/*.tgz ./helm_cache/
‘./chartexample/chartexample-0.1.0.tgz’ -> ‘./helm_cache/chartexample-0.1.0.tgz’
$ cd helm_cache
$ helm repo index .
$ helm repo add cache file://$PWD/
"cache" has been added to your repositories
$ helm search repo chartexample
NAME                    CHART VERSION   APP VERSION     DESCRIPTION
cache/chartexample      0.1.0           1.16.0          A Helm chart for Kubernetes
$ helm repo list
NAME    URL
cache   file:///home/zoobab/soft/helm_cache/
```

Not that the list of helm repositories starts with a `file:///`:

```
$ helm repo list
NAME    URL
cache   file:///home/zoobab/soft/helm_cache/
```

The `index.yaml` should look like this, look at the `urls` field that does not contain `http`:

```
apiVersion: v1
entries:
  chartexample:
  - apiVersion: v2
    appVersion: 1.16.0
    created: "2022-10-18T12:20:54.858719098+02:00"
    description: A Helm chart for Kubernetes
    digest: c262f7269459773bac53470649470b78b72a72bac6571b0931c8456c6bfc5ee1
    name: chartexample
    type: application
    urls:
    - chartexample-0.1.0.tgz
    version: 0.1.0
generated: "2022-10-18T12:20:54.857888206+02:00"
```

Tested with helm version 3.10:

```
$ helm version
version.BuildInfo{Version:"v3.10.1", GitCommit:"9f88ccb6aee40b9a0535fcc7efea6055e1ef72c9", GitTreeState:"clean", GoVersion:"go1.18.7"}
```

## Links

* https://medium.com/htc-research-engineering-blog/a-simple-example-for-helm-chart-fbb5c7208e94
