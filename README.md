# Helm plugin for file://

This plugin adds basic support for local repositories to helm.

Example:
```
$ helm plugin add https://github.com/zoobab/helm_file_repo
$ mkdir helm_cache
$ cd helm_cache
# helm pull or cp locally created tgz files here.
$ helm repo index .
$ helm repo add cache file://$PWD/
$ helm search repo ...
```

