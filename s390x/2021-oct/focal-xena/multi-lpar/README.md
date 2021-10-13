Tempest validation of OpenStack focal-xena (OVS) on s390x

The single tempest smoke failure is caused by
[a known issue](https://bugs.launchpad.net/charm-keystone/+bug/1830076) that we
have been observing
[since bionic-ussuri](../../../2020-jun/bionic-ussuri/multi-lpar/).
