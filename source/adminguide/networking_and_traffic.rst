.. 
   "Option One Technologies Cloud" (OOTC) documentation.


About Networking in OOTC
---------------------------

OOTC implements flexible virtual networking solution. 
A virtual network in OOTC can be L2 or L3. When creating a VM, you 
can select the networks, the VM has to connect. You can also connect a running VM to a new 
virtual network.


L3 Networks
~~~~~~~~~~~~~~~~~

..
   @Question: Considering the end-users point of view, I am considering isolated networks as 
   L3 networks. Is this OK?

An L3 network can be connected to the Internet via loadbalancer or NAT.
VMs in an L3 network can be assigned with IP addresses via DHCP.

To create an L3 Network:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Networks in Network menu. |network-icon.png|

#. Click Add network. Provide the following information:

   -  **Name**: The name of the network..

   -  **Description**: The description of the network..

   -  **Zone**. The name of the zone this network applies to. Each zone
      is a broadcast domain, and therefore each zone has a different IP
      range for the guest network. The administrator must configure the
      IP range for each zone.

   -  **Network offering**: Select one of the avialable offerings.

..
   @Todo: Need to include some desscription about each of the offerings.

   -  **Gateway**: The gateway that the VMs should use.

   -  **Netmask**: The netmask of the subnet assigned to the network.

   -  **Network Domain**.

..
   @Question: What should be the description here?

#. Click OK to create network.


L2 Networks
~~~~~~~~~~~

L2 networks do not have routing capabilities. OOTC will not assign IP addresses to L2 networks.
You can use L2 networks for internal communciation of VMs.

To create an L2 Network:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Networks in Network menu. |network-icon.png|

#. Click Add network and select L2 tab. Provide the following information:

   -  **Name**: The name of the network..

   -  **Description**: The description of the network..

   -  **Zone**. The name of the zone this network applies to. Each zone
      is a broadcast domain, and therefore each zone has a different IP
      range for the guest network. The administrator must configure the
      IP range for each zone.

   -  **Network offering**: Select one of the avialable offerings.

#. Click OK to create network.


Managing Networks
~~~~~~~~~~~~~~~~~

To view VM instances connected to a network:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Networks in Network menu. |network-icon.png|

#. Click on the network name in the list of networks.

#. Click View Instances button.

To connect a VM to a network:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Instances from Compute menu. |compute-icon.png|

#. Click on NICs tab. Click on Add network to VM.

#. Select the network from the drop-down menu.

#. Optionally, provide an IP address.

#. Click OK.

To remove a connection to a network from a VM:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Instances from Compute menu. |compute-icon.png|

#. Click on NICs tab.

#. In the list of networks displayed, click on the plus icon |plus-icon.png| of the network you
   wish to remove.

#. Click on Delete button. |delete-button.png|


To delete a network:

#. Log in to the CloudStack UI.

#. In the left navigation, choose Guest Networks in Network menu. |network-icon.png|

#. Click on the network name in the list of networks.

#. Click View Instances button, and make sure that the network has no virtual NICs attached.

#. In the network view, click Delete button. |delete-button.png|


.. include:: networking/multiple_ips_on_single_nic.rst


..
   @Question: Is elastic IP assignment supported?

..
   @Question: are security groups supported?



.. include:: networking/virtual_private_cloud_config.rst

