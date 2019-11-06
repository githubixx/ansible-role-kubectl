ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `8.0.0+1.14.1` means this is release `8.0.0` of this role and it's meant to be used with Kubernetes version `1.14.x`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------

see [CHANGELOG](https://github.com/githubixx/ansible-role-kubectl/blob/master/CHANGELOG.md)

Role Variables
--------------

```
# "kubectl" version to install
kubectl_version: "1.15.5"
# SHA512 checksum of the archive (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG-1.15.md
# for the checksums)
kubectl_checksum: "sha512:e462587773345695e3d2e2faba53d0bf4a57ab6fe5ae69e5f253fe8529247d05d36d2b8ea6cf5f60dd9c805e29f8385cd42b25d79576248544f26511dc98626b"
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
