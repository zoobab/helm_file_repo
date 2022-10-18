# Helm plugin for file://

This plugin adds basic support for local repositories to helm.

Example:
```
$ git clone https://github.com/zoobab/helm_file_repo
$ helm plugin add ./helm_file_repo
Installed plugin: file
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
```

## Links

* https://medium.com/htc-research-engineering-blog/a-simple-example-for-helm-chart-fbb5c7208e94
