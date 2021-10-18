Tempest validation of OpenStack focal-xena (OVN) on s390x

The [initial tempest smoke run](tempest_smoke.txt) had two failures:

* `test_default_domain_exists`'s failure is caused by
  [a known issue](https://bugs.launchpad.net/charm-keystone/+bug/1830076) that
  we have been observing
  [since bionic-ussuri](../../../2020-jun/bionic-ussuri/multi-lpar/).
* `test_schedule_to_all_nodes` failed because our small test lab was running
  out of disk space. We re-ran that specific test to be on the
  safe side and [it finally fully passed](tempest_smoke2.txt).

The compute and OVN central nodes point to a
[special PPA](https://launchpad.net/~corey.bryant/+archive/ubuntu/focal-xena)
containing an early bugfix for
[lp:1947003](https://bugs.launchpad.net/ubuntu/+source/ovn/+bug/1947003) which
hasn't been officially released yet.
