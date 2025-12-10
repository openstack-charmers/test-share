Tempest validation of OpenStack noble-flamingo (OVN) on s390x.

The Tempest smoke tests have detected the following bugs:

- [LP: #2043987 - Nova - unsupported configuration: machine type 's390-ccw-virtio-mantic' does not support ACPI](https://launchpad.net/bugs/2043987)

- [LP: #2114021 - Glance - Unsupported Media Type 0 The request media type application/octet-stream is not supported by this server](https://bugs.launchpad.net/charm-glance/+bug/2114021)

These applications were patched, after which all smoke tests passed. Tests were run with the Tempest option `--serial` to force sequentially-run tests due to system resource constraints.

