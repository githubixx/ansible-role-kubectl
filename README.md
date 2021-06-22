ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `14.0.0+1.20.2` means this is release `14.0.0` of this role and `kubectl` client binary version is `1.20.2`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

Changelog
---------

see [CHANGELOG](https://github.com/githubixx/ansible-role-kubectl/blob/master/CHANGELOG.md)

Role Variables
--------------

```yaml
---
# "kubectl" version to install
kubectl_version: "1.21.2"

# The default "archive" will download "kubectl" as a ".tar.gz" file. This is
# about 2.5x smaller then "binary" but the tarball needs to be unarchived
# by the role first after downloading.
# If you specify "binary" the "kubectl" binary file will be downloaded. In
# contrast to the tarball the binary file is about 2.5x bigger but doesn't
# need to be unarchived by this role.
# If download file size is important for you (e.g. slow download or download
# over mobile link) stay with "archive". Otherwise "binary" might be an option.
kubectl_download_filetype: "binary"
# SHA512 checksum of the .tar.gz file (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.21.md#client-binaries)
kubectl_checksum_archive: "sha512:0d744eec49354250a43510efc4d911a4b67f3b36dc62c28e2b852e31e9d00e474d0f44287c5b89ccbafcaa91ed1ecaa12a881a25984aa6e33fdf5c55141e9349"
# SHA512 checksum of the binary (see https://storage.googleapis.com/kubernetes-release/release/v1.21.2/bin/linux/amd64/kubectl.sha512)
kubectl_checksum_binary: "sha512:fbd688840426d312dc5930f83c427d428559b2e3eca4c95cc39fb47fde960829bfe0dbb9ccf49ec80799ef013dbb0f4f1dc7aec59678d444b88eda8168fd77a9"

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

This will setup two Docker container with Ubuntu 20.04 and 18.04 with `kubectl` installed. So you should be able to execute the following commands if everything worked well:

```bash
docker exec -it test-ubuntu-2004 kubectl version --client=true
Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.2", GitCommit:"faecb196815e248d3ecfb03c680a4507229c2a56", GitTreeState:"clean", BuildDate:"2021-01-13T13:28:09Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"linux/amd64"}

docker exec -it test-ubuntu-1804 kubectl version --client=true
Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.2", GitCommit:"faecb196815e248d3ecfb03c680a4507229c2a56", GitTreeState:"clean", BuildDate:"2021-01-13T13:28:09Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"linux/amd64"}
```

To clean up run

```bash
molecule destroy
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
