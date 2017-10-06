ansible-role-kubectl
====================

Installs kubectl command line utility used to interact with the Kubernetes API Server.

Versions
--------

I tag every release and try to stay with semantic versioning. If you want to use the role I recommend to checkout the latest tag. The master branch is basically development while the tags mark stable releases. But in general I try to keep master in good shape too.

v1.8.0 - update default kubectl to v1.8.0
v1.0.0 - initial release

Role Variables
--------------

```
kubectl_version: 1.8.0
kubectl_bin_directory: /usr/local/bin
kubectl_owner: root
kubectl_group: root
kubectl_os: linux # use "darwin" for MacOS X
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
