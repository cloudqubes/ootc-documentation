.. 
   "Option One Technologies Cloud" (OOTC) documentation.


Using Multiple Guest Networks
-----------------------------



Adding an Additional Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click Add guest network. Provide the following information:

   -  **Name**: The name of the network. This will be user-visible.

   -  **Display Text**: The description of the network. This will be
      user-visible.

   -  **Zone**. The name of the zone this network applies to. Each zone
      is a broadcast domain, and therefore each zone has a different IP
      range for the guest network. The administrator must configure the
      IP range for each zone.

   -  **Network offering**: If the administrator has configured multiple
      network offerings, select the one you want to use for this
      network.

   -  **Guest Gateway**: The gateway that the guests should use.

   -  **Guest Netmask**: The netmask in use on the subnet the guests
      will use.

#. Click Create.


Reconfiguring Networks in VMs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack provides you the ability to move VMs between networks and
reconfigure a VM's network. You can remove a VM from a network and add
to a new network. You can also change the default network of a virtual
machine. With this functionality, hybrid or traditional server loads can
be accommodated with ease.

This feature is supported on XenServer, VMware, and KVM hypervisors.


Prerequisites
^^^^^^^^^^^^^

Ensure that vm-tools are running on guest VMs for adding or removing
networks to work on VMware hypervisor.


Adding a Network
^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the VM that you want to work with.

#. Click the NICs tab.

#. Click Add network to VM.

   The Add network to VM dialog is displayed.

#. In the drop-down list, select the network that you would like to add
   this VM to.

   A new NIC is added for this network. You can view the following
   details in the NICs page:

   -  ID

   -  Network Name

   -  Type

   -  IP Address

   -  Gateway

   -  Netmask

   -  Is default

   -  CIDR (for IPv6)


Removing a Network
^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the VM that you want to work with.

#. Click the NICs tab.

#. Locate the NIC you want to remove.

#. Click Remove NIC button. |remove-nic.png|

#. Click Yes to confirm.


Selecting the Default Network
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the VM that you want to work with.

#. Click the NICs tab.

#. Locate the NIC you want to work with.

#. Click the Set default NIC button. |set-default-nic.png|.

#. Click Yes to confirm.

Changing the Network Offering on a Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A user or administrator can change the network offering that is
associated with an existing guest network.

#. Log in to the CloudStack UI as an administrator or end user.

#. If you are changing from a network offering that uses the CloudStack
   virtual router to one that uses external devices as network service
   providers, you must first stop all the VMs on the network.

#. In the left navigation, choose Network.

#. Click the name of the network you want to modify.

#. In the Details tab, click Edit. |edit-icon.png|

#. In Network Offering, choose the new network offering, then click
   Apply.

   A prompt is displayed asking whether you want to keep the existing
   CIDR. This is to let you know that if you change the network
   offering, the CIDR will be affected.

   If you upgrade between virtual router as a provider and an external
   network device as provider, acknowledge the change of CIDR to
   continue, so choose Yes.

#. Wait for the update to complete. Don't try to restart VMs until the
   network change is complete.

#. If you stopped any VMs, restart them.


.. |remove-nic.png| image:: /_static/images/remove-nic.png
   :alt: button to remove a NIC.
.. |set-default-nic.png| image:: /_static/images/set-default-nic.png
   :alt: button to set a NIC as default one.
.. |edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit.
