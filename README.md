ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `7.0.0+1.13.0` means this is release `7.0.0` of this role and it's meant to be used with Kubernetes version `1.13.0`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------


Role Variables
--------------

```
# "kubectl" version to install
kubectl_version: "1.13.0"
# SHA512 checksum of the archive (for "kubernetes-client-linux-amd64.tar.gz" by default).
# See https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG-1.13.md for the checksums.
kubectl_checksum: "sha512:61a6cd3b1fb34507e0b762a45da09d88e34921985970a2ba594e0e5af737d94c966434b4e9f8e84fb73a0aeb5fa3e557344cd2eb902bf73c67d4b4bff33c6831"
# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"
# Directory to store the kubeclient archive
kubectl_tmp_directory: "{{ lookup('env', 'TMPDIR') | default('/tmp',true) }}"
# Owner of "kubectl" binary
kubectl_owner: "root"
# Group of "kubectl" binary
kubectl_group: "root"
# Operarting system on which "kubectl" should run on
kubectl_os: "linux" # use "darwin" for MacOS X, "windows" for Windows
# Processor architecture "kubectl" should run on
kubectl_arch: "amd64" # other possible values: "386","arm64","arm","ppc64le","s390x"
```

Example Playbook
----------------

```
- hosts: your-host
  roles:
    - githubixx.kubectl
```

License
-------

GNU GENERAL PUBLIC LICENSE Version 3

Author Information
------------------

http://www.tauceti.blog
