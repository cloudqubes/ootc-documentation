.. 
   "Option One Technologies Cloud" (OOTC) documentation.



About Virtual Networks
---------------------------

OOTC offers, you a flexible virtual networking solution. 
A virtual network in OOTC can be L2 or L3.


L3 Networks
~~~~~~~~~~~~~~~~~

An L3 network can be connected to the Internet via loadbalancer or NAT router.

L2 Networks
~~~~~~~~~~~

L2 networks do not have routing capabilities. OOTC will not assign IP addresses to L2 networks.
You can use L2 networks for internal communciation of VMs.




Network Offerings
-----------------

.. note:: 
   For the most up-to-date list of supported network services, see the 
   OOTC UI or call listNetworkServices.

A network offering is a named set of network services, such as:

-  DHCP

-  DNS

-  Source NAT

-  Static NAT

-  Port Forwarding

-  Load Balancing

-  Firewall

-  VPN

-  (Optional) Name one of several available providers to use for a given
   service, such as Juniper for the firewall

-  (Optional) Network tag to specify which physical network to use

When creating a new VM, the user chooses one of the available network
offerings, and that determines which network services the VM can use.


When creating a new virtual network, the OOTC administrator
chooses which network offering to enable for that network. Each virtual
network is associated with one network offering. A virtual network can
be upgraded or downgraded by changing its associated network offering.
If you do this, be sure to reprogram the physical network to match.



.. |L2-networks-gui.JPG| image:: /_static/images/L2-networks-gui.JPG
   :alt: Creating L2 network from GUI
