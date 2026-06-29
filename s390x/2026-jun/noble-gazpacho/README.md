# Sunbeam Gazpacho validation on Noble/s390x

This directory contains the validation report for a single-LPAR Sunbeam
OpenStack Gazpacho deployment on Ubuntu Noble/s390x.

Unlike the previous charmed-openstack validation, this run used the newer
Sunbeam architecture: Kubernetes charms for the OpenStack control plane, with a
small machine-plane model for the s390x hypervisor and storage services.

The test covered the core cloud services: Keystone, Glance, Placement, Nova,
Neutron/OVN, Cinder with MicroCeph, and a real s390x QEMU hypervisor. Optional
services such as Swift, Horizon, Octavia, Manila, Designate, Ironic, Watcher,
and telemetry were not part of this validation.

## Deployment substrate

The control plane ran on a single-node Canonical K8s cluster with Calico
networking, Kubernetes local persistent volumes for control-plane state, and a
LoadBalancer address for the Sunbeam API endpoint. MicroCeph provided the
OpenStack Cinder block-storage backend.

## Result summary

- Ubuntu series: `noble`
- OpenStack series: `gazpacho`
- Architecture: `s390x`
- Run ID: `20260625T150834Z`
- Hypervisor: `special18`, QEMU, `up`
- Guest image: Ubuntu 24.04 s390x cloud image
- Guest boot: passed
- Floating-IP SSH: passed
- Cinder volume create/attach: passed
- Tempest smoke: `Ran: 131`, `Passed: 98`, `Skipped: 33`, `Failed: 0`

The skipped Tempest tests are for services or capabilities intentionally outside
this core deployment, such as Swift, Horizon, Manila, Designate, Ironic,
Watcher, VPNaaS, QoS, and some validation/multinode scenarios.

## Notable upstream issues and mitigations

- Nova can emit ACPI/APIC features for s390x libvirt guests, which is
  not supported by the `s390-ccw-virtio` machine type. The validation used a
  hypervisor configuration that avoided this guest-boot failure.
- SPICE graphics are not supported by the s390x QEMU build used here, so SPICE
  was disabled for the hypervisor.
- `juju_status.txt` shows `cinder-router` app-level `waiting` on a database
  offer, while the unit is active; Cinder API, volume create, and volume attach
  validation passed.

## Evidence files

Key evidence is in `juju_status.txt`, `openstack_origin.txt`,
`hypervisor_list.txt`, `ceph_tests.txt`, `instance_launch.txt`,
`instance_ssh.txt`, and `tempest_smoke.txt`.

## Interpretation

This is a representative validation of the core Sunbeam/OpenStack data plane on
Noble/s390x using the Kubernetes-charm-based Sunbeam architecture. It is not a
validation of optional OpenStack services that were not deployed.
