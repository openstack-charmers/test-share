Tempest validation of OpenStack jammy-zed (OVS) on s390x.

The tempest smoke tests have passed successfully on this configuration with
the following bugs that required a workaround:

- [LP: #1994083 - os-brick - "FileNotFoundError: \[Errno 2\] No such file or directory" is raised when dmidecode is not installed](https://launchpad.net/bugs/1994083)
- [LP: #1962381 - charm-nova-compute - Nova Instance Creation Fails with Error: USB is diabled for this domain](https://launchpad.net/bugs/1962381)
