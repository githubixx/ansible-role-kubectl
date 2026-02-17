# ansible-role-kubectl

Installs `kubectl` command line utility used to interact with the Kubernetes API Server.

## Versions

I tag every release and try to stay with [semantic versioning](http://semver.org). If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too. A tag `26.0.0+1.35.1` means this is release `26.0.0` of this role and `kubectl` client binary version is `1.35.1`. If the role itself changes `X.Y.Z` before `+` will increase. If the Kubernetes version changes `X.Y.Z` after `+` will increase. This allows to tag bugfixes and new major versions of the role while it's still developed for a specific Kubernetes release.

## Changelog

**Change history:**

See full [CHANGELOG](https://github.com/githubixx/ansible-role-kubectl/blob/master/CHANGELOG.md)

**Recent changes:**

## 26.0.0+1.35.1

- update kubectl to `v1.35.1`

## 25.0.0+1.34.4

- update kubectl to `v1.34.4`
- replace injected `ansible_*` facts usage with `ansible_facts[...]` (prepares for ansible-core 2.24 where `INJECT_FACTS_AS_VARS` default changes)

## 24.0.2+1.33.8

- update kubectl to `v1.33.8`
- Download URL `cdn.dl.k8s.io` doesn't work anymore. Changed it to `dl.k8s.io`
- Molecule: add `Debian 13` / change download URL to `dl.k8s.io`

## 24.0.1+1.33.5

- update `README.md`

## 24.0.0+1.33.5

- **Potential breaking change**: `kubectl_tmp_directory` default value changed from `{{ lookup('env', 'TMPDIR') | default('/tmp', true) }}` to `{{ ansible_facts['env']['TMPDIR'] | default('/tmp', true) }}`. The old implementation looked up `TMPDIR` variable on the Ansible controller. But that was not the intention here. The new default uses the `TMPDIR` value of the remote machine where `kubectl` should be installed. If you set this variable on your own nothing will change for you. And even if you use the default setting chances are low that you notice the change. Still, please test if this change affects you (contribution by @fhennig).
- update kubectl to `v1.33.5`

## 23.4.0+1.32.7

- update kubectl to `v1.32.7`
- removed Ubuntu 20.04 because reached end of life
- add `.gitignore`

## 23.3.0+1.31.5

- update kubectl to `v1.31.5`

## 23.2.0+1.30.5

- update kubectl to `v1.30.5`
- Download URL of `kubectl` archive has changed. `https://storage.googleapis.com` doesn't work anymore. Using `https://dl.k8s.io` instead now (see [Client Binaries](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.30.md#client-binaries)).
- update `.yamllint`
- update `meta/main.yml`
- Molecule: update tests
- Molecule: fix various `ansible-lint` issues

## Installation

- Directly download from Github (Change into Ansible roles directory before cloning. You can figure out the role path by using `ansible-config dump | grep DEFAULT_ROLES_PATH` command):
`git clone https://github.com/githubixx/ansible-role-kubectl.git githubixx.kubectl`

- Via `ansible-galaxy` command and download directly from Ansible Galaxy:
`ansible-galaxy install role githubixx.kubectl`

- Create a `requirements.yml` file with the following content (this will download the role from Github) and install with
`ansible-galaxy role install -r requirements.yml` (change `version` if needed):

```yaml
---
roles:
  - name: githubixx.kubectl
    src: https://github.com/githubixx/ansible-role-kubectl.git
    version: 26.0.0+1.35.1
```

## Role Variables

```yaml
# "kubectl" version to install
kubectl_version: "1.35.1"

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
# SHA512 checksum of the "kubernetes-client-linux-amd64.tar.gz" file
# (see https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.32.md#client-binaries)
kubectl_checksum_archive: "sha512:0dc7ccca28a4272147de370af7d429b86426faf3c2ded1241c33a57c12f13d728cc207b7c2a46f0dfd28b46bdfde7152bc15afc446dd5a41ce3b14f882614dbb"

#
# SHA512 checksum of the binary. There is normally no need to change it.
# Further information:
#   - https://kubernetes.io/releases/download/#binaries
#   - https://www.downloadkubernetes.com/
kubectl_checksum_binary: "sha512:https://dl.k8s.io/release/v{{ kubectl_version }}/bin/{{ kubectl_os }}/{{ kubectl_arch }}/kubectl.sha512"

# Where to install "kubectl" binary
kubectl_bin_directory: "/usr/local/bin"

# Directory to store the kubectl archive
kubectl_tmp_directory: "{{ ansible_facts['env']['TMPDIR'] | default('/tmp', true) }}"

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

## Testing

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

This will setup a few Docker container with Ubuntu 22.04/24.04 and Debian 11/12 with `kubectl` installed. To verify if everything worked:

```bash
molecule verify
```

To clean up run

```bash
molecule destroy
```

## Example Playbook

```yaml
- hosts: your-host
  roles:
    - githubixx.kubectl
```

## License

GNU GENERAL PUBLIC LICENSE Version 3

## Author Information

[TauCeti Blog](http://www.tauceti.blog)
