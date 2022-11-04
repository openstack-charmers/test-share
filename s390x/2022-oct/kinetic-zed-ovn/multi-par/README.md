Tempest validation of OpenStack kinetic-zed (OVN) on s390x.

The tempest smoke tests have passed successfully on this configuration with
the following bugs that required a workaround:

- [LP: #1994083 - os-brick - "FileNotFoundError: \[Errno 2\] No such file or directory" is raised when dmidecode is not installed](https://launchpad.net/bugs/1994083)
- [LP: #1962381 - charm-nova-compute - Nova Instance Creation Fails with Error: USB is diabled for this domain](https://launchpad.net/bugs/1962381)
- [LP: #1995735 - neutron - neutron.privileged.agent.linux.ip_lib.InterfaceOperationNotSupported: Operation not supported on interface](https://launchpad.net/bugs/1995735)
- [LP: #1995738 - neutron - ORM session: SQL execution without transaction in progress](https://launchpad.net/bugs/1995738)
