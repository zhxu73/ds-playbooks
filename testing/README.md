# testing

This folder contains the test harness for the DS playbooks. It consists of a
simplified Data Store and a playbook runner.

__TODO__ Multiple testing environments need to be created for different
situations.

## The Environment

The environment consists of seven containers. The `amqp` container hosts the
RabbitMQ broker that in turn hosts the `irods` exchange, where the Data Store
publishes messages to. The `dbms` container hosts the PostgreSQL server that in
turn hosts the ICAT DB. The `load_balancer` container hosts the HAProxy for the
IES. The `ies_centos6` container hosts the IES running CentOS 6. The
`ies_centos7` container hosts the IES running CentOS 7. The `rs_centos6`
container hosts the resource server running on CentOS 6. Finally, the
`rs_centos7` container hosts the resource server running on CentOS 7.

## Building the Harness

There are two convenience scripts for building the docker images for the
environment. `build` builds all the required images, and `clean` deletes them.

## Testing

`run` is a convenience script for running a playbook against the test
environment. This script will bring up the environment, run the playbook and
any tests, and then tear down the environment. It performs the tests in the
following order.

1. It performs a syntax checkout on the playbook under test.
1. It runs the playbook on the testing inventory.
1. If there are any tests of the playbook, it runs those tests.
1. It performs an idempotency check of the playbook.

Tests can be defined for a given playbook. They should be placed in a playbook
with the same name inside a `tests` folder that is in the same folder as the
playbook under test.
