Tempest validation of OpenStack noble-dalmatian (OVN) on s390x.

The tempest smoke tests have detected the following bugs:

- [LP: #2043987 - Nova - unsupported configuration: machine type 's390-ccw-virtio-mantic' does not support ACPI](https://launchpad.net/bugs/2043987)

This was patched after which all smoke tests passed.
