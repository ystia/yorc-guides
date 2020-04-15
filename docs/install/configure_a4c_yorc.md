# Configure Alien4Cloud to use Yorc

To configure Alien4Cloud to use Yorc, you need to:

* create, configure, enable the orchestrator in Alien4Cloud.

To create a new orchestrator, select now menus `Administration` > `Orchestrators` to get this page :

![A4C New Yorc Orchestrator](../images/a4cNewOrchestrator.png)

Click on `New Orchestrator`, enter `Yorc` as the orchestrator name, and select the Yorc plugin like below :

![A4C Create New Yorc Orchestrator](../images/a4cCreateOrchestrator.png)

Click on `Create`, a new Orchestrator is created :

![A4C New Yorc Orchestrator Created](../images/a4cOrchestratorCreated.png)

Select this orchestrator, a page appears showing the Orchestrator is in state `Disabled` for now.
Select menu `Configuration` on the left hand side, a page appears where you can
provide the URL to connect to your Yorc Server :

![A4C Configure Yorc Orchestrator](../images/a4cYorcConfigure.png)

In the field `urlYorc`, enter a URL like `http://<your host IP address>:8800`.
Once done, select the menu `Information` on the left hand side to get this page :

![A4C Yorc Orchestrator Info](../images/a4cYorcInfo.png)

Click on `Enable`. Alien4Cloud will attempt to connect to Yorc and if everything
goes well, the Orchestrator should then appear as `Connected` :

![A4C New Yorc Orchestrator Connected](../images/a4cYorcConnected.png)

Alien4Cloud is now configured to use your Yorc Server.

The next step is to [configure deployment locations](configure_a4c_yorc_locations.md):
Google Cloud, OpenStack, AWS, Slurm, Hosts Pools.
