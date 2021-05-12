# Bootstrap a full orchestration stack

You can bootstrap a full orchestration stack that includes:

* Consul
* Terraform
* Ansible
* Yorc
* Vault
* Alien4Cloud

By running a single command. All you need to do is to download the Yorc binary, run it and describe the environment
on which Yorc should be setup. Supported environment are for now:

* AWS
* GCP
* OpenStack
* Any existing host with an SSH server thanks to HostsPool

Then Yorc will automatically download all required components, and run a deployment on the target infrastructure.
This could be used to quickly deploy a development environment or a fully HA and secured setup.

For more information on this feature please read the [bootstrap documentation](https://yorc.readthedocs.io/en/v4.1.1/bootstrap.html).
