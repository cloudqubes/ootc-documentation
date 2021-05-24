.. 
   "Option One Technologies Cloud" (OOTC) documentation.
   


Virtual Private Cloud
--------------------


OOTC Virtual Private Cloud is a private, isolated environment.
A VPC can have its own virtual network topology that
resembles a traditional physical network. You can launch VMs in the
virtual network that can have private addresses in the range of your
choice, for example: 10.0.0.0/16. You can define network networks within
your VPC network range, which in turn enables you to group similar kinds
of instances based on IP address range.

For example, if a VPC has the private range 10.0.0.0/16, its guest
networks can have the network ranges 10.0.1.0/24, 10.0.2.0/24,
10.0.3.0/24, and so on.


Adding a Virtual Private Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. Log in to the OOTC UI.

#. In the left navigation, choose Guest Networks in Network menu. |network-icon.png|

#. Click Add VPC. The Add VPC page is displayed as follows:

   |add-vpc.png|

   Provide the following information:

   -  **Name**: A short name for the VPC that you are creating.

   -  **Description**: A brief description of the VPC.

   -  **Zone**: Choose the zone where you want the VPC to be available.

   -  **CIDR**: Defines the CIDR range for all
      the networks (guest networks) within a VPC. When you create a network,
      ensure that its CIDR is within this CIDR value you enter. The
      CIDR must be RFC1918 compliant.

   -  **Network Domain**:

..
   @Question: What should be the description of the domain.

   -  **VPC Offering**": Select an offering according to your requirement.

#. Click OK.


Adding Networks to the VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~

You can create multiple networks within a VPc. A network inside a VPC, is not visible to other VPCs.

To add a network to a VPC:

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. In the Select view, select VPC.

   All the VPC that you have created for the account is listed in the
   page.

#. Click on the Networks tab.

#. Click Add network.

#. Specify the following:

   All the fields are mandatory.

   -  **Name**: A unique name for the network you create.

   -  **Network Offering**: Select a network offering as required.

..
   @Question: Need to include descriptions of Network Offerings configured.

   -  **Gateway**: The gateway for the network. 


   -  **Netmask**: The netmask for the network.

      For example, if the VPC CIDR is 10.0.0.0/16 and the network network
      CIDR is 10.0.1.0/24, the gateway of the network is 10.0.1.1, and the
      netmask of the network is 255.255.255.0.

   -  **ACL**: Choose an ACL to be applied for VMs in this network.

#. Click OK.



.. _conf-net-acl:

Configuring Network Access Control List
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Define Network Access Control List (ACL) on the VPC virtual router to
control incoming (ingress) and outgoing (egress) traffic between the VPC
networks, and the networks and Internet. By default, all incoming traffic to
the guest networks is blocked and all outgoing traffic from guest
networks is allowed, once you add an ACL rule for outgoing traffic, then
only outgoing traffic specified in this ACL rule is allowed, the rest is
blocked. To open the ports, you must create a new network ACL. 

About Network ACL Lists
^^^^^^^^^^^^^^^^^^^^^^^

In OOTC terminology, Network ACL is a group of Network ACL items.
Network ACL items are nothing but numbered rules that are evaluated in
order, starting with the lowest numbered rule. These rules determine
whether traffic is allowed in or out of any network associated with the
network ACL. You need to add the Network ACL items to the Network ACL,
then associate the Network ACL with a network within the VPC. Each network can be
associated with only one ACL.


Creating ACL Lists
^^^^^^^^^^^^^^^^^^

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. Click on the name of the VPC.

#. Select Network ACL Lists.

   The following default rules are displayed in the Network ACLs page:
   default\_allow, default\_deny.

#. Click Add ACL Lists, and specify the following:

   -  **ACL List Name**: A name for the ACL list.

   -  **Description**: A short description of the ACL list that can be
      displayed to users.


Creating an ACL Rule
^^^^^^^^^^^^^^^^^^^^

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. Click on the name of the VPC.

#. Select Network ACL Lists tab.

#. Select the desired ACL list.

#. Select the ACL List Rules tab.

   To add an ACL rule, fill in the following fields to specify what kind
   of network traffic is allowed in the VPC.

   -  **Rule Number**: The order in which the rules are evaluated.

   -  **CIDR**: The CIDR acts as the Source CIDR for the Ingress rules,
      and Destination CIDR for the Egress rules. To accept traffic only
      from or to the IP addresses within a particular address block,
      enter a CIDR or a comma-separated list of CIDRs. The CIDR is the
      base IP address of the incoming traffic. For example,
      192.168.0.0/22. To allow all CIDRs, set to 0.0.0.0/0.

   -  **Action**: What action to be taken. Allow traffic or block.

   -  **Protocol**: The networking protocol that sources use to send
      traffic to the network. The TCP and UDP protocols are typically used
      for data exchange and end-user communications. The ICMP protocol
      is typically used to send error messages or network monitoring
      data. All supports all the traffic. Other option is Protocol
      Number.

   -  **Start Port**, **End Port** (TCP, UDP only): A range of listening
      ports that are the destination for the incoming traffic. If you
      are opening a single port, use the same number in both fields.

   -  **Protocol Number**: The protocol number associated with IPv4 or
      IPv6. For more information, see `Protocol Numbers 
      <http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>`_.

   -  **ICMP Type**, **ICMP Code** (ICMP only): The type of message and
      error code that will be sent.

   -  **Traffic Type**: The type of traffic: Incoming or outgoing.

#. Click Add. The ACL rule is added.

   You can edit the tags assigned to the ACL rules and delete the ACL
   rules you have created. Click the appropriate button in the Details
   tab.


Creating a network with Custom ACL List
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a VPC.

#. Create a custom ACL list.

#. Add ACL rules to the ACL list.

#. Create a network in the VPC.

   Select the desired ACL list while creating a network.

#. Click OK.


Assigning a Custom ACL List to a network
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a VPC.

#. Create a network in the VPC.

#. Associate the network with the default ACL rule.

#. Create a custom ACL list.

#. Add ACL rules to the ACL list.

#. Select the network for which you want to assign the custom ACL.

#. Click the Replace ACL List icon. |replace-acl-icon.png|

   The Replace ACL List dialog is displayed.

#. Select the desired ACL list.

#. Click OK.


Deploying VMs to the Networks in a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. From the list of VPCs, click on the desired VPC.

#. Click on the Networks tab.

#. Click on the Instances and click on Add Instance button.

   The Add Instance page is displayed.

   Follow the on-screen instruction to add an instance. For information
   on adding a VM instance, see the `“Creating VMs” <virtual_machines.html#creating-vms>`_.


Acquiring a New IP Address for a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you acquire an IP address, all IP addresses are allocated to VPC,
not to the guest networks within the VPC. The IPs are associated to the
guest network only when the first port-forwarding, load balancing, or
Static NAT rule is created for the IP or the network. IP can't be
associated to more than one network at a time.

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. From the list of VPCs, click on the desired VPC.

#. Click on Public IP Addresses tab.

   The Public IP Addresses page is displayed.

#. Click Acquire New IP, and click Yes in the confirmation dialog.

   You are prompted for confirmation because, typically, IP addresses
   are a limited resource. Within a few moments, the new IP address
   should appear with the state Allocated. You can now use the IP
   address in port forwarding, load balancing, and static NAT rules.


Releasing an IP Address Alloted to a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The IP address is a limited resource. If you no longer need a particular
IP, you can disassociate it from its VPC and return it to the pool of
available addresses. An IP address can be released, only
when all the networking rules are removed for this IP address. 
The released IP address will still belongs to the same VPC.

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. From the list of VPCs, click on the desired VPC.

#. Click on Public IP Addresses tab.

   The Public IP Addresses page is displayed.

#. From the list of IP addresses, click the Release IP button |release-ip-icon.png|
   of the IP address you wish to release.

#. In the Details tab, click the Release IP button |release-ip-icon.png|


Removing Networks in VPC
~~~~~~~~~~~~~~~~~~~~~~~~

You can remove a network from a VPC. A removed network cannot be revoked. When
a network is removed, only the resources of the network are expunged. All the
network rules (port forwarding, load balancing and staticNAT) and the IP
addresses associated to the network are removed. The IP address still be
belonging to the same VPC.

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. From the list of VPCs, click on the desired VPC.

#. Click on the Networks tab.

#. Select the network you want to remove.

#. Click the Delete Network button.
   |del-network.png|

   Click Yes to confirm. Wait for some time for the network to be removed.


Editing, Restarting, and Removing a Virtual Private Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Ensure that all the networks are removed before you remove a VPC.

#. Log in to the OOTC UI.

#. In the left navigation, choose VPC in Network menu. |network-icon.png|

#. From the list of VPCs, click on the desired VPC.

#. You can edit the name and description of a VPC. To do that, select
   the VPC, then click the Edit button. |vpc-edit-icon.png|

   To restart a VPC, select the VPC, then click the Restart button.
   |restart-vpc.png|

   To remove the VPC, click the Remove VPC button |remove-vpc.png|.


.. |add-vpc.png| image:: /_static/images/add-vpc.png
   :alt: adding a vpc.
.. |add-network.png| image:: /_static/images/add-network.png
   :alt: adding a network to a vpc.
.. |replace-acl-icon.png| image:: /_static/images/replace-acl-icon.png
   :alt: button to replace an ACL list
.. |add-new-gateway-vpc.png| image:: /_static/images/add-new-gateway-vpc.png
   :alt: adding a private gateway for the VPC.
.. |add-vm-vpc.png| image:: /_static/images/add-vm-vpc.png
   :alt: adding a VM to a vpc.
.. |addvm-network-sharednw.png| image:: /_static/images/addvm-network-sharednw.png
   :alt: adding a VM to a VPC network and shared network.
.. |release-ip-icon.png| image:: /_static/images/release-ip-icon.png
   :alt: button to release an IP.
.. |enable-disable.png| image:: /_static/images/enable-disable.png
   :alt: button to enable Static NAT.
.. |select-vmstatic-nat.png| image:: /_static/images/select-vm-staticnat-vpc.png
   :alt: selecting a network to apply staticNAT.
.. |vpc-lb.png| image:: /_static/images/vpc-lb.png
   :alt: Configuring internal LB for VPC
.. |del-network.png| image:: /_static/images/del-network.png
   :alt: button to remove a network
.. |vpc-edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit.
.. |remove-vpc.png| image:: /_static/images/remove-vpc.png
   :alt: button to remove a VPC
.. |restart-vpc.png| image:: /_static/images/restart-vpc.png
   :alt: button to restart a VPC
