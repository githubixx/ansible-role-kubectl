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
kubectl_version: "1.19.4"

# The default "archive" will download "kubectl" as a ".tar.gz" file. This is
# about 2.5x smaller then "binary" but the tarball needs to be unarchived
# by the role first after downloading.
# If you specify "binary" the "kubectl" binary file will be downloaded. In
# contrast to the tarball the binary file is about 2.5x bigger but doesn't
# need to be unarchived by this role.
# If download file size is important for you (e.g. slow download or download
# over mobile link) stay with "archive". Otherwise "binary" might be an option.
kubectl_download_filetype: "binary"
# SHA512 checksum of the .tar.gz file (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.19.md#client-binaries)
kubectl_checksum_archive: "sha512:7e65358a19b4eabfbbf886061098d7edc1268ab59a3e0f813a264ff525bed8c76f4f0bd5bcb151d8a05dcb1b2f25d874e2346d448725e701614439a27f960079"
# SHA512 checksum of the binary (see https://storage.googleapis.com/kubernetes-release/release/v1.18.5/bin/linux/amd64/kubectl.sha512)
kubectl_checksum_binary: "sha512:a0f0b68116f2bcf9469a569070829c5d0f10231df2b3f53c672e8b0ffb8ccf3112e89bc330bc74692171889c93d74b664cf960dd1925ca3a9b242ebba33e2ee5"

# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"

# Directory to store the kubeclient archive
kubectl_tmp_directory: "{{ lookup('env', 'TMPDIR') | default('/tmp',true) }}"

# Owner of "kubectl" binary
kubectl_owner: "root"

# Group of "kubectl" binary
kubectl_group: "root"

# Specifies the permissions of the "kubectl" binary
kubectl_binary_mode: "0755"

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
