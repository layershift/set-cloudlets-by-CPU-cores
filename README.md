# About

This is a [Jelastic Cloud Scripting](https://docs.cloudscripting.com/) manifest example showing how to adjust the Jelastic cloudlet limit for nodes in the `cp` (application server) layer to provide 4 CPU cores.

Jelastic limits CPU by MHz according to the number of cloudlets added to each node (1 cloudlet = 128MB RAM + 400MHz CPU). The hardware capabilities of the underlying CPU(s) determine how many cores are exposed to the Jelastic node (Virtuozzo container).

# Usage

Execute the Cloud Script using any of the following methods:
* Use the [Import](https://docs.jelastic.com/environment-import/) button in your Jelastic dashboard
* Use the [Install](https://docs.jelastic.com/api/#!/api/marketplace.Jps-method-Install) API request
* Use the [Install](https://docs.jelastic.com/cli-install-jps/) CLI request

# Known limitations

CPU clock speed exposed in `/proc/cpuinfo` is dynamic according to the virtualisation limits applied, so a precise calculation is not possible from inside the container. The manifest provides a workaround for this by setting the cloudlet limits at the calculated value for 5 cores, and then decrementing the cloudlet limit until only 4 cores are visible.

The calculation only considers `node[0]` and assumes all other nodes within the layer are on identical hardware - depending on hosting provider platform specifics, the hardware hosting other nodes might be different.