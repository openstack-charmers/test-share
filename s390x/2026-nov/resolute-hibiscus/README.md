# Sunbeam Hibiscus validation on Resolute on s390x

This directory contains the validation report for Sunbeam OpenStack Hibiscus
deployment on Ubuntu Resolute on a single-LPAR s390x machine.

Compared with the previous Resolute/Gazpacho validation, this run moves the OVN
networking component to the machine plane, using `microovn` and
`sunbeam-ovn-proxy` to replace the control-plane `ovn-central` and `ovn-relay`
charms. The provider bridge is managed by `openstack-network-agents`. Currently,
the machine plane also runs `microceph`, `cinder-volume`, and
`openstack-hypervisor`.

The test covered the core cloud services: Keystone, Glance, Placement, Nova,
Neutron/OVN, Cinder with MicroCeph, and a s390x QEMU hypervisor. Optional
services such as Swift, Horizon, Octavia, Manila, Designate, Ironic, Watcher,
and telemetry were not part of this validation.

## Test mechanism

The deployment and validation scripts can be found in the `sunbeam/` directory of `zopenstack` repository: <https://github.com/ubuntu-openstack/zopenstack>.

## Deployment substrate

The control plane was deployed on a single-node Canonical Kubernetes cluster
with Calico CNI plugin networking, local persistent volumes for the
control-plane state, and a LoadBalancer service for the Sunbeam API endpoint.
MicroCeph provided the block-storage backend for OpenStack Cinder.

The machine plane ran `microovn`, `sunbeam-ovn-proxy`,
`openstack-network-agents`, `microceph`, `cinder-volume`, and
`openstack-hypervisor`. The run used `CHARM_SOURCE=hybrid`, with local s390x
builds for the `cinder-volume-ceph`, `microceph`,
`microcluster-token-distributor`, `rabbitmq-k8s`, and `sunbeam-machine` charms.
Local s390x snaps were also built and run for `cinder-volume` and
`openstack-hypervisor`.

## Source provenance

This report includes `source_provenance.txt`, which records the checksums of
local charms and snaps as well as the metadata for OCI images used. Each OCI
image entry lists its local or remote reference, digest, platform, and the
workload that consumes it.

Detailed package versions for those workload images are recorded in
`image_package_versions.txt`.

## Result summary

- Ubuntu series: `resolute` (26.04.1 LTS)
- OpenStack series: `hibiscus` (2026.2)
- Architecture: `s390x`
- Run ID: `20261117T185714Z`
- Hypervisor: `special19`, QEMU, `up`
- Guest image: Ubuntu 26.04 s390x cloud image
- Guest boot: passed
- Floating-IP SSH: passed
- Cinder volume create/attach: passed
- Tempest smoke: `Ran: 135`, `Passed: 100`, `Skipped: 35`, `Failed: 0`

Compared with the Resolute/Gazpacho run, Hibiscus passes two additional Tempest
tests (`100` vs `98`) with the same `135` run and zero failures. The two
additional passing tests are:

- `neutron_tempest_plugin.api.admin.test_tag.TagFilterQosPolicyTestJSON.test_filter_qos_policy_tags`
- `neutron_tempest_plugin.api.admin.test_tag.TagQosPolicyTestJSON.test_qos_policy_tags`

No Gazpacho-passing test regressed in this run.

The skipped Tempest tests are for services or capabilities intentionally outside
this core deployment, such as Swift, Horizon, Manila, Designate, Ironic,
Watcher, VPNaaS, Octavia traffic validation, and multinode scenarios.

## Notable upstream issues and mitigations

- Tempest tests were run serially to avoid resource pressure on the single
  LPAR.
- Resolute's distro Tempest plugin set emitted Watcher deprecation warnings;
  these did not affect the smoke result.
- SPICE and vTPM are disabled for the s390x QEMU hypervisor because the current
  libvirt/QEMU build does not support them.

## Evidence files

Key evidence is in `juju_status.txt`, `openstack_origin.txt`,
`hypervisor_list.txt`, `ceph_tests.txt`, `image_list.txt`,
`image_package_versions.txt`, `instance_launch.txt`, `instance_ssh.txt`,
`source_provenance.txt`, and `tempest_smoke.txt`.

The guest booted as `s390x-verify-server` on `special19`, received
`192.168.222.188`, and was reachable over floating IP `10.13.3.219`:

```text
SSH works
s390x
PRETTY_NAME="Ubuntu 26.04.1 LTS"
```

## Interpretation

This is a representative validation of the core Sunbeam/OpenStack data plane on
Resolute/s390x using the Kubernetes-charm-based Sunbeam architecture. It is not
a validation of optional OpenStack services that were not deployed.
