# Install Yorc manually

To install Yorc manually, you will have to install Yorc dependencies:

* Ansible 2.7.9
* Hashicorp Terraform 0.11.8
* Hashicorp Consul 1.2.3

See a detailed description of these installations at <https://yorc.readthedocs.io/en/v4.1.1/install.html>.

You will have then to configure the Yorc server, through environment variables,
command-line flags, or a configuration file just like what was described in
section [Install Yorc the easy way (docker)](install_yorc_docker.md).

Each configuration parameter is described at <https://yorc.readthedocs.io/en/v4.1.1/configuration.html>

You could then just start a Consul agent then Yorc as described at <https://yorc.readthedocs.io/en/v4.1.1/run.html>

Or if you plan to install Yorc in High Availability mode, follow this guide : <https://yorc.readthedocs.io/en/v4.1.1/ha.html>.

Once Yorc is installed, you can go to the next section on how to [install the UI companion of Yorc, Alien4Cloud](install_a4c.md).
