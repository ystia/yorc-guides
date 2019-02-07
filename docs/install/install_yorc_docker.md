# Install Yorc using docker

## Prerequisite

Install docker following the [Docker installation guide](https://docs.docker.com/install/).

If your setup is behind proxies, you will need to define proxies if you want to
upload upload images from external repositories.

For example on CentOS, you could create a file `/etc/systemd/system/docker.service.d/http-proxy.conf`
with this content :

```systemd
[Service]
Environment="HTTP_PROXY=http://10.1.2.3:8080" "NO_PROXY=10.1.2.4,docker-registry.somecorporation.com"
```

Then flush changes and restart docker:

```bash
systemctl daemon-reload
systemctl restart docker
```

## Yorc configuration

Before running a Yorc docker container, you will have to define its configuration.
It can be done through different ways, that you can combine:

* command line flags
* environment variables
* a configuration file

Command line flags take precedence over environment variables, which take precedence
over values defined in the configuration file.

See [Yorc Server configuration](https://yorc.readthedocs.io/en/v3.1.1/configuration.html)
documentation for details on how to configure the Yorc server using these three different methods.

This section will show the use of a configuration file.
Create a file $HOME/yorc/config.yorc.yaml (json is supported as well), configuring
the Yorc server so that it can deploy applications on different infrastructures,
Google Cloud, OpenStack, AWS, Kubernetes, Slurm:

```yaml
# Prefix on Compute Nodes that will be created on demand
resources_prefix: yorc-
infrastructures:
  # Google Cloud configuration
  google:
    application_credentials: /etc/yorc/gcloud/my-project-service-account.json
    project: my-project
  # OpenStack Infrastructure settings
  openstack:
    auth_url: http://10.1.2.3:5000/v2.0
    tenant_name: mytenant
    user_name: myuser
    password: mypasswd
    region: RegionOne
    private_network_name: private-net
    default_security_groups: [secgroup1,secgroup2]
  # AWS Infrastructure
  aws:
    region: us-east-2
    access_key: ABCDEFABCEDFABCEDFAB
    secret_key: lkipwrbmh+NDcoIVPChYgOcC/a8FfXPwhGZNOGWT
  # Kubernetes Infrastructure settings
  kubernetes:
    ca_file: /etc/yorc/kubernetes/ca.pem,
    cert_file: /etc/yorc/kubernetes/client.crt
    key_file: /etc/yorc/kubernetes/client.key
    master_url: https://10.1.2.40:6443
  # Slurm Infrastructure setting
  slurm:
    user_name: root
    private_key: /etc/yorc/slurm_private_key
    url: 10.1.2.30
    port: 22
# Ansible configuration
# Here using ssh instead of default paramiko for better performances
ansible:
  debug: true
  use_openssh: true
  keep_operation_remote_path: true
  keep_generated_recipes: true
  hosted_operations:
    unsandboxed_operations_allowed: true
```

All properties defined above are described in the  [Yorc Server configuration](https://yorc.readthedocs.io/en/v3.1.1/configuration.html) documentation.

Note that Infrastructure parameters above are provided in plain text, but it is possible
to keep them secret by storing them in a vault.
See Yorc documentation on Hashicorp vault [integration](https://yorc.readthedocs.io/en/v3.1.1/vault.html) and [configuration](https://yorc.readthedocs.io/en/v3.1.1/configuration.html#option-hashivault).

One type of infrastructure is not defined here, this is the Hosts Pool infrastructure.

The Hosts Pool infrastructure allows to register existing Compute nodes into a pool managed by Yorc.
These compute nodes could be physical or virtual machines, containers or whatever as long as Yorc can SSH into it.
You can add new nodes to the Hosts Pool at any time (or remove some, provided they are not allocated to a deployed application).

Nodes can be declared in a file, that you can modify at any time to add new nodes
to the Hosts Pool, modify nodes descriptions, or remove some nodes provided these nodes to remove are not allocated to a deployed application.

Here is an example of a file declaring two hosts :

```yaml
hosts:
- name: host1
  connection:
    user: myuser
    private_key: /etc/yorc/secrets/id_rsa
    host: 10.198.1.10
    port: 22
  labels:
    environment: dev
    host.cpu_frequency: 3 GHz
    host.disk_size: 40 GB
    host.mem_size: 4GB
    host.num_cpus: "2"
    os.architecture: x86_64
    os.distribution: centos
    os.type: linux
    os.version: "7.3.1611"
    private_address: "10.0.0.33"
    public_address: "10.198.1.10"
    public_ip_address: "10.198.1.10"
- name: host2
  connection:
    user: cloud-user
    private_key: /etc/yorc/secrets/id_rsa
    host: 10.198.1.11
    port: 22
  labels:
    environment: dev
    host.cpu_frequency: 3 GHz
    host.disk_size: 40 GB
    host.mem_size: 4GB
    host.num_cpus: "2"
    os.architecture: x86_64
    os.distribution: centos
    os.type: linux
    os.version: "7.3.1611"
    private_address: "10.0.0.36"
    public_address: "10.198.1.11"
    public_ip_address: "10.198.1.11"
```

You can apply this definition, running this command:

```bash
yorc hostspool apply mypooldefinition.yaml
```

## Start Yorc server

Now that the configuration file `$HOME/yorc/config.yorc.yaml` was created, the Yorc server
container can be started. This container expects to read its configuration from a
file under `/etc/yorc` within the container (or from environment variables or CLI flags as explained above).

So we will mount the host directory `$HOME/yorc` as `/etc/yorc` on the container.
And use the image of Yorc 3.1.1 stored on docker hub at <https://hub.docker.com/r/ystia/yorc/>.
The port 8800 used by Yorc by default needs also to be exported.
It gives this command to start Yorc:

```bash
docker run -d \
  --mount "type=bind,src=/home/cloud-user/yorc,dst=/etc/yorc" \
  -p 8800:8800 --rm --name yorc --hostname yorc ystia/yorc:3.1.1
```

You can then see and follow Yorc server logs running this command:

```bash
docker logs --follow yorc
```

You can enter the container running :

```bash
docker exec -it yorc bash
```

Then start using yorc CLI :

```bash
$ yorc help
yorc is the main command, used to start the http server.
Yorc is a new generation orchestrator.  
It is cloud-agnostic, flexible and secure.

Usage:
  yorc [flags]
  yorc [command]

Available Commands:
  deployments Perform commands on deployments
  help        Help about any command
  hostspool   Perform commands on hosts pool
  server      Perform the server command
  version     Print the version

Flags:
  -h, --help   help for yorc

Use "yorc [command] --help" for more information about a command.
```

See more details in the documentation on [Running Yorc in a docker container](https://yorc.readthedocs.io/en/v3.1.1/docker.html)

Yorc is now installed.

You can skip next section on [installing Yorc manually](install_yorc_manually.md),
and go to the section on how to [install the UI companion of Yorc, Alien4Cloud](install_a4c.md).
