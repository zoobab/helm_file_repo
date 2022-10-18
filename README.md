# Helm plugin for file://

This plugin adds basic support for local repositories to helm.

Example:
```
$ helm plugin add https://github.com/zoobab/helm_file_repo
$ helm create chartexample
$ cd chatexample
$ helm package .
$ cd ..
$ mkdir helm_cache
$ cd helm_cache
$ cp ../chartexample/*.tgz .
$ helm repo index .
$ helm repo add cache file://$PWD/
$ helm search repo chartexample
```

