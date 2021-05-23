.. 
   "Option One Technologies Cloud" (OOTC) documentation.



Configuring Multiple IP Addresses on a Single NIC
-------------------------------------------------

OOTC provides you the ability to associate multiple private IP
addresses per guest VM NIC. In addition to the primary IP, you can
assign additional IPs to the guest VM NIC. This feature is supported on
all the network configurations: Basic, Advanced, and VPC. Security
Groups, Static NAT and Port forwarding services are supported on these
additional IPs.

As always, you can specify an IP from the guest subnet; if not
specified, an IP is automatically picked up from the guest VM subnet.
You can view the IPs associated with for each guest VM NICs on the UI.
You can apply NAT on these additional guest IPs by using network
configuration option in the OOTC UI. You must specify the NIC to
which the IP should be associated.


Use Cases
~~~~~~~~~

Some of the use cases are described below:

-  Network devices, such as firewalls and load balancers, generally work
   best when they have access to multiple IP addresses on the network
   interface.

-  Moving private IP addresses between interfaces or instances.
   Applications that are bound to specific IP addresses can be moved
   between instances.

-  Hosting multiple SSL Websites on a single instance. You can install
   multiple SSL certificates on a single instance, each associated with
   a distinct IP address.


Guidelines
~~~~~~~~~~

To prevent IP conflict, configure different subnets when multiple
networks are connected to the same VM.


Assigning Additional IPs to a VM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the OOTC UI.

#. In the left navigation bar, click Instances in the compute menu. |compute-icon.png|

#. Click the name of the instance you want to work with.

#. In the Details tab, click NICs. Click on the plus sign at the network interface that
   you want to add the secondary IP.

#. Click View Secondary IPs.

#. Click Edit Secondary IPs. |edit-secondary-ip-icon.png|

#. Enter the new IP address and click on Add Secondary IP.

   You need to configure the IP on the guest VM NIC manually. OOTC
   will not automatically configure the acquired IP address on the VM.
   Ensure that the IP address configuration persist on VM reboot.

   Within a few moments, the new IP address should appear with the state
   Allocated. You can now use the IP address in Port Forwarding or
   StaticNAT rules.

