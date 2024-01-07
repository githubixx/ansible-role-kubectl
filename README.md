ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `23.0.2+1.28.5` means this is release `23.0.2` of this role and `kubectl` client binary version is `1.28.5`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------

see [CHANGELOG](https://github.com/githubixx/ansible-role-kubectl/blob/master/CHANGELOG.md)

Role Variables
--------------

```yaml
# "kubectl" version to install
kubectl_version: "1.28.5"

# The default "binary" will download "kubectl" as a binary file. This is
# about 2.5x bigger then the ".tar.gz" file. The tarball needs to be unarchived
# by the role first after downloading and is smaller.
#
# If you specify "binary" the "kubectl" binary file will be downloaded. In
# contrast to the tarball the binary file is about 2.5x bigger but doesn't
# need to be unarchived by this role.
#
# If download file size is important for you (e.g. slow download or download
# over mobile link) stay with "archive". Otherwise "binary" might be an option.
kubectl_download_filetype: "binary"
#
# SHA512 checksum of the .tar.gz file (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.28.md#client-binaries)
kubectl_checksum_archive: "sha512:9cd61a97b37cb27cc565f5a2cebd6086b86148c5759eb0e6a0c03e7be4b701bec407c46a65633c51a00a7aa74733c2fdd082b9da3382d38525e2e5b8dbb11b77"
#
# SHA512 checksum of the binary. There is normally no need to change it.
# Further information:
#   - https://kubernetes.io/releases/download/#binaries
#   - https://www.downloadkubernetes.com/
kubectl_checksum_binary: "sha512:https://cdn.dl.k8s.io/release/v{{ kubectl_version }}/bin/{{ kubectl_os }}/{{ kubectl_arch }}/kubectl.sha512"

# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"

# Directory to store the kubectl archive
kubectl_tmp_directory: "{{ lookup('env', 'TMPDIR') | default('/tmp', true) }}"

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

This will setup a few Docker container with Ubuntu 20.04/22.04 and Debian 11/12 with `kubectl` installed. To verify if everything worked:

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
