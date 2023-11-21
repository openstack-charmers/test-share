Tempest validation of OpenStack mantic-bobcat (OVN) on s390x.

The tempest smoke tests have passed successfully on this configuration with the
following bugs detected:

- [LP: #2039225 - Horizon - django.core.cache.backends.memcached.MemcachedCache backend is removed](https://launchpad.net/bugs/2039225)
- [LP: #2039226 - Horizon - cannot import name 'ugettext_lazy' from 'django.utils.translation'](https://launchpad.net/bugs/2039226)
- [LP: #2043987 - Nova - unsupported configuration: machine type 's390-ccw-virtio-mantic' does not support ACPI](https://launchpad.net/bugs/2043987)
