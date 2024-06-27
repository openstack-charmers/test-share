Tempest validation of OpenStack noble-caracal (OpenVSwitch) on s390x.

The tempest smoke tests have passed successfully on this configuration with the
following bugs detected:

- [LP: #2043987 - Nova - unsupported configuration: machine type 's390-ccw-virtio-mantic' does not support ACPI](https://launchpad.net/bugs/2043987)
