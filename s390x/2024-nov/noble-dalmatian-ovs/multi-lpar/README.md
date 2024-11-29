Tempest validation of OpenStack noble-dalmatian (OVS) on s390x.

The tempest smoke tests have detected the following bugs:

- [LP: #2043987 - Nova - unsupported configuration: machine type 's390-ccw-virtio-mantic' does not support ACPI](https://launchpad.net/bugs/2043987)

This was patched after which all smoke tests passed apart from `tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes` which failed due to lack of resources on the four hyperviusors deployed.

Running this test separately subsequently passed:

    $ tempest run --config-file etc/tempest.conf --regex tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes
    {0} tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes [40.538224s] ... ok

