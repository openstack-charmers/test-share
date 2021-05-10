Tempest validation of OpenStack hirsute-wallaby (OVS) on s390x

The [initial tempest smoke run](tempest_smoke.txt) had two (non-)failures:

* `test_default_domain_exists`'s failure is caused by
  [a known issue](https://bugs.launchpad.net/charm-keystone/+bug/1830076) that
  we have been observing
  [since bionic-ussuri](../../../2020-jun/bionic-ussuri/multi-lpar/).
* `AccountQuotasTest` passed but we seem to have had a hiccup while the test
  was tearing down (cleaning up). We re-ran that specific test to be on the
  safe side and [it finally fully passed](tempest_smoke2.txt).
