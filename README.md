ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org) (well kind of...). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `r1.0.0_v1.8.0` means this is release 1.0.0 of this role and it's meant to be used with Kubernetes version 1.8.0. If the role itself changes `rX.Y.Z` will increase. If the Kubernetes version changes `vX.Y.Z` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------

**r3.0.0_v1.10.4**

- update default kubectl to v1.10.4

**r2.0.2_v1.9.1**

- update default kubectl to v1.9.1
- changed download location
- add checksum
- allow more options to download binaries for different architectures

**r1.0.2_v1.8.0**

- update default kubectl to v1.8.0

Role Variables
--------------

```
# "kubectl" version to install
kubectl_version: "1.10.4"
# SHA256 checksum of the archive (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG-1.10.md
# for the checksums
kubectl_checksum: "sha256:2831fe621bf1542a1eac38b8f50aa40a96b26153e850b3ff7155e5ce4f4f400e"
# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"
# Directory to store the kubeclient archive
kubectl_tmp_directory: "{{lookup('env', 'TMPDIR') | default('/tmp',true)}}"
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
