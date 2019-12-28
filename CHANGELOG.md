Changelog
---------

**10.1.0+1.16.3**

- use `remote_src: yes` for unarchive

**10.0.0+1.16.3**

- update default kubectl to v1.16.3

**9.0.1+1.15.5**

- update default kubectl to v1.15.5

**No version change**

- Because Ansible Galaxy only allows tags using semantic versioning format I had to change some older tags. If you really rely on that old tags the following tag names changed:

```
r1.0.0_v1.8.0  -> 1.0.0+1.8.0
r1.0.2_v1.8.0  -> 1.0.2+1.8.0
r2.0.0_v1.9.1  -> 2.0.0+1.9.1
r2.0.1_v1.9.1  -> 2.0.1+1.9.1
r2.0.2_v1.9.1  -> 2.0.2+1.9.1
r3.0.0_v1.10.4 -> 3.0.0+1.10.4
r3.0.1_v1.10.4 -> 3.0.1+1.10.4
r3.0.2_v1.10.8 -> 3.0.2+1.10.8
r5.0.0_v1.12.0 -> 5.0.0+1.12.0
r5.0.1_v1.12.1 -> 5.0.1+1.12.1
r6.0.0_v1.13.0 -> 6.0.0+1.13.0
r6.0.1_v1.13.0 -> 6.0.1+1.13.0
```

The commits (the SHA1) behind the tags are still the same of course.

**9.0.0+1.15.3**

- update default kubectl to v1.15.3

**8.0.3+1.14.6**

- update README

**8.0.2+1.14.6**

- update default kubectl to v1.14.6

**8.0.1+1.14.2**

- update default kubectl to v1.14.2

**8.0.0+1.14.1**

- update default kubectl to v1.14.1

**7.1.1+1.13.2**

- add link to CHANGELOG in README

**7.1.0+1.13.2**

- update default kubectl to v1.13.2
- `kubectl_owner` and `kubectl_group` now used (previous version always used user `root` and group `root`)

**7.0.0+1.13.0**

- use correct semantic versioning as described in https://semver.org. Needed for Ansible Galaxy importer as it now insists on using semantic versioning.
- moved changelog entries to separate file
- make Ansible linter happy
- no major changes but decided to start a new major release as versioning scheme changed quite heavily

**r6.0.0_v1.13.0**

- update default kubectl to v1.13.0

**r5.0.1_v1.12.1**

- update default kubectl to v1.12.1

**r5.0.0_v1.12.0**

- update default kubectl to v1.12.0

**r4.0.0_v1.11.3**

- update default kubectl to v1.11.3

**r3.0.2_v1.10.8**

- update default kubectl to v1.10.8

**r3.0.1_v1.10.4**

- Ubuntu 18.04 supported
- update README

**r3.0.0_v1.10.4**

- update default kubectl to v1.10.4

**r2.0.2_v1.9.1**

- update default kubectl to v1.9.1
- changed download location
- add checksum
- allow more options to download binaries for different architectures

**r1.0.2_v1.8.0**

- update default kubectl to v1.8.0
