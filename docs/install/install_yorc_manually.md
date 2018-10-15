# Install Yorc manually

To install Yorc manually, you will have to install Yorc dependencies:
  * ansible 2.4.1.0
  * Hashicorp Terraform 0.9.11
  * Hashicorp Consul 1.0.6

See a detailed description of these installations at https://yorc.readthedocs.io/en/v3.0.1/install.html.

You will have then to configure the Yorc server, through environment variables,
command-line flags, or a configuration file just like what was described in 
section [Install Yorc the easy way (docker)](docs/install/install_yorc_docker.md).

Each configuration parameter is described at https://yorc.readthedocs.io/en/v3.0.1/configuration.html

You could then just start a Consul agent then Yorc as described at https://yorc.readthedocs.io/en/v3.0.1/run.html

Or if you plan to install Yorc in High Availability mode, follwing this guide : https://yorc.readthedocs.io/en/v3.0.1/ha.html
