# Ystia Orchestrator guides

This repository provides guidance on how to install, use and troubleshoot the Ystia Orchestrator (Yorc) latest release 4.0.0.

## Overview

The Ystia Orchestrator provides applications lifecycle management over hybrid infrastructures​:

* Infrastructure as a Service (Google Cloud, AWS, OpenStack, Hosts Pool)​
* Container as a Service (Kubernetes)​
* High Performance Computing (Slurm)

Applications and Components are written in [TOSCA](http://docs.oasis-open.org/tosca/TOSCA-Simple-Profile-YAML/v1.2/TOSCA-Simple-Profile-YAML-v1.2.html)
(Topology and Orchestration Specification for Cloud Applications), an OASIS consortium
standard language  to describe a topology of cloud based web services, their
components and relationships, portable across infrastructures.

The Orchestrator has companions products :

* the [Ystia Forge](https://github.com/ystia/forge/tree/v2.2.0/org/ystia), repository of components and application templates
* A UI/Studio [Alien4Cloud](https://github.com/alien4cloud/alien4cloud/tree/2.2.0), that can use Yorc to deploy these application templates.

Yorc is one binary used for both the CLI and the Yorc server exposing a REST API.

To get started, you can start running a Yorc docker container, install Alien4Cloud,
upload sample application from the Forge and deploy this application on one of the
supported types of infrastructures as described in the following sections.

## Installation/configuration

### Install the Ochestrator

* [Install Yorc the easy way (docker)](docs/install/install_yorc_docker.md)
* [Install Yorc manually](docs/install/install_yorc_manually.md)

### Install and configure the Orchestrator UI companion - Alien4Cloud

* [Install Alien4Cloud](docs/install/install_a4c.md)
* [Configure Alien4Cloud to use Yorc](docs/install/configure_a4c_yorc.md)
* [Configure deployment locations](docs/install/configure_a4c_yorc_locations.md)

### Bootstrap a full stack

* [Bootstrap an full Orchestration Stack in one command](docs/install/bootstrap.md)

### Applications deployment

* [Upload Components/Application templates](docs/applications/upload_from_forge.md) from Ystia Forge
* [Create and deploy an application](docs/applications/create_deploy.md)

### Troubleshooting

* [Troubleshooting an application deployment failure](docs/troubleshooting/troubleshoot-deployment.md)
