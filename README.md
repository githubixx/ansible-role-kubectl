ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `20.0.0+1.25.0` means this is release `20.0.0` of this role and `kubectl` client binary version is `1.25.0`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------

see [CHANGELOG](https://github.com/githubixx/ansible-role-kubectl/blob/master/CHANGELOG.md)

Role Variables
--------------

```yaml
---
# "kubectl" version to install
kubectl_version: "1.25.5"

# The default "archive" will download "kubectl" as a ".tar.gz" file. This is
# about 2.5x smaller then "binary" but the tarball needs to be unarchived
# by the role first after downloading.
# If you specify "binary" the "kubectl" binary file will be downloaded. In
# contrast to the tarball the binary file is about 2.5x bigger but doesn't
# need to be unarchived by this role.
# If download file size is important for you (e.g. slow download or download
# over mobile link) stay with "archive". Otherwise "binary" might be an option.
kubectl_download_filetype: "binary"
# SHA512 checksum of the .tar.gz file (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.25.md#client-binaries)
kubectl_checksum_archive: "sha512:c229b5700944f86f8312cb76d44248de813b8bae58026ec137b3e19bf422e91ed9848115bd549c5d5915b43acd639db71c2e9ece756c1b1c4f706672e11151b6"
# SHA512 checksum of the binary (see https://storage.googleapis.com/kubernetes-release/release/v1.25.5/bin/linux/amd64/kubectl.sha512)
kubectl_checksum_binary: "sha512:c62099f1022f924b8f95ce3adc7588f0b2a3a0194959484b2b7c8b156d4391ae4a6c53e216655a062048f9bf6622c74410d369c979561d260c4e4d4785b525c8"

# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"

# Directory to store the kubectl archive
kubectl_tmp_directory: "{{ lookup('env', 'TMPDIR') | default('/tmp',true) }}"

# Owner of "kubectl" binary
kubectl_owner: "root"

# Group of "kubectl" binary
kubectl_group: "root"

# Specifies the permissions of the "kubectl" binary
kubectl_binary_mode: "0755"

# Operating system on which "kubectl" should run on
kubectl_os: "linux"  # use "darwin" for MacOS X, "windows" for Windows

# Processor architecture "kubectl" should run on
kubectl_arch: "amd64"  # other possible values: "386","arm64","arm","ppc64le","s390x"
```

Testing
-------

This role has a small test setup that is created using [molecule](https://github.com/ansible-community/molecule). To run the tests follow the molecule [install guide](https://molecule.readthedocs.io/en/latest/installation.html). Also ensure that a Docker daemon runs on your machine.

Assuming [Docker](https://www.docker.io) is already installed you need at least two Python packages:

```bash
pip3 install --user molecule
pip3 install --user molecule-docker
```

Afterwards molecule can be executed:

```bash
molecule converge
```

This will setup a few Docker container with Ubuntu 18.04 + 20.04 and Debian 10 + 11 with `kubectl` installed. To verify if everything worked:

```bash
molecule verify
```

To clean up run

```bash
molecule destroy
```

Example Playbook
----------------

```yaml
- hosts: your-host
  roles:
    - githubixx.kubectl
```

License
-------

GNU GENERAL PUBLIC LICENSE Version 3

Author Information
------------------

[TauCeti Blog](http://www.tauceti.blog)
