# Configure a HostsPool Cloud location

From Alien4Cloud UI, select menus `Administration` > `Orchestrators`, then select
the orchestrator `Yorc`.
A page appears where you can select `Location(s)` on the left hand side :

![A4C Yorc Locations](../images/a4cYorcLocations.png)

Click on `New Location`. Enter a name: `Hosts Pool`. Select the Infrastructure type
`HostsPool`:

![A4C Yorc Locations HostsPool](../images/a4cCreateHostsPool.png)

Click on `Create`. A page appears allowing to configure this location, select the
menu `On demand resources` like below :

![A4C Yorc Locations On Demand Resources](../images/a4cHPOnDemandResources.png)

To add an on-demand Compute Node, drag the `yorc.nodes.hostspool.Compute` component
on the right hand side cell,
and drop this component to the left hand side cell, to get this :

![A4C Yorc Locations HostsPool New Compute Resource](../images/a4cHPNewResource.png)

You can select the property shareable if you want to make this compute node shareable,
so that different deployments could use this same resource.

Credentials don't have to be defined here. For hosts in a Hosts Pool, credentials
are defined in the Yorc server configuration as described in the [installation section](../install/install_yorc_docker.md).

Next step is to [upload Components/Application templates](../applications/upload_from_forge.md)
from the Ystia Forge.
