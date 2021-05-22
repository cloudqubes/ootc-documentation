.. 
   "Option One Technologies Cloud" (OOTC) documentation.
   
About Working with Virtual Machines
===================================

OOTC gives you complete control over the
lifecycle of the guest VMs in the cloud. You can start, reboot, stop, and
destroy a VM using the OOTC UI.

A VM can have a name, a display name, and a group. You can use these to 
keep your VMs organized.
..
   @Question: The group is visible only at the VM creation. Should we mention that in the docs?


A VMs can be configured to be Highly Available (HA). An HA-enabled
VM is monitored by the system. If the system detects that the VM is
down, it will attempt to restart the VM, possibly on a different host.
..
   @Question: Must link to 'how to enable HA in a VM'. OOTC docs does not clearly
   explain how to enable HA. Can you mention whether HA is supported in OOTC?
   I could not find any parameters in the UI related to enabling HA.

A VM is allocated one public IP address. When the VM is started,
OOTC automatically creates a static NAT between this public IP
address and the private IP address of the VM.

If elastic IP is in use (with the NetScaler load balancer), the IP
address initially allocated to the new VM is not marked as elastic. The
user must replace the automatically configured IP with a specifically
acquired elastic IP, and set up the static NAT mapping between this new
IP and the guest VM’s private IP. The VM’s original IP address is then
released and returned to the pool of available public IPs. Optionally,
you can also decide not to allocate a public IP to a VM in an
EIP-enabled Basic zone. For more information on Elastic IP, see
`“About Elastic IP” <networking/elastic_ips.html>`_.

..
   @Question: Assume above behavior is same in OOTC. Please confirm?

OOTCcannot distinguish a guest VM that was shut down by the user
(such as with the “shutdown” command in Linux) from a VM that shut down
unexpectedly. If an HA-enabled VM is shut down from inside the VM,
OOTC will restart it. To shut down an HA-enabled VM, you must go
through the OOTC UI or API.


VM Lifecycle
============

Virtual machines can be in the following states:

- Created
- Running
- Stopped
- Destroyed
- Expunged

With the intermediate states of

- Creating
- Starting
- Stopping
- Expunging


Creating VMs
------------

Virtual machines are usually created from a template. You can also
create blank virtual machines. A blank virtual machine is a virtual
machine without an OS template. You can attach an ISO file and install
the OS from the CD/DVD-ROM.

.. note:: 
   You can create a VM without starting it. You can determine whether the 
   VM needs to be started as part of the VM deployment. A request parameter, 
   startVM, in the deployVm API provides this feature. For more information, 
   see the Developer's Guide.

To create a VM from a template:

#. Log in to the OOTC UI.

#. In the left navigation bar, click Instances.

#. Click Add Instance.

#. Select a zone. 

#. Select a template, then follow the steps in the wizard. For more
   information about how the templates came to be in this list, see
   `*Working with Templates* <templates.html>`_.

#. Be sure that the hardware you have allows starting the selected
   service offering.

#. Click Submit and your VM will be created and started.

To create a VM from an ISO:

#. Log in to the OOTC UI .

#. In the left navigation bar, click Instances.

#. Click Add Instance.

#. Select a zone. 

#. Select ISO Boot, and follow the steps in the wizard.

#. Click Submit and your VM will be created and started.



Install Required Tools and Drivers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Be sure the following are installed on each VM:

-  For XenServer, install PV drivers and Xen tools on each VM. This will
   enable live migration and clean guest shutdown. Xen tools are
   required in order for dynamic CPU and RAM scaling to work.


To be sure that Xen tools or VMware Tools is installed, use one of the
following techniques:

-  Create each VM from a template that already has the tools installed;
   or,

-  When registering a new template, the user can
   indicate whether tools are installed on the template. This can be
   done through the UI or using the updateTemplate API; or,

..
   @Question: Is above related to 'Install Required Tools and Drivers' required?



Accessing VMs
-------------


To access a VM through the OOTC UI:

#. Log in to the OOTC UI.

#. Click Instances, then click the name of a running VM.

#. Click the View Console button |console-icon.png|.

To access a VM directly over the network:

#. The VM must have some port open to incoming traffic. For example, in
   a basic zone, a new VM might be assigned to a security group which
   allows incoming traffic. This depends on what security group you
   picked when creating the VM. In other cases, you can open a port by
   setting up a port forwarding policy. See `“IP
   Forwarding and Firewalling” <advanced_zone_config.html#ip-forwarding-and-firewalling>`_.

#. If a port is open but you can not access the VM using ssh, it’s
   possible that ssh is not already enabled on the VM. This will depend
   on whether ssh is enabled in the template you picked when creating
   the VM. Access the VM through the OOTC UI and enable ssh on the
   machine using the commands for the VM’s operating system.

#. If the network has an external firewall device, you will need to
   create a firewall rule to allow access. See `“IP
   Forwarding and Firewalling” <advanced_zone_config.html#ip-forwarding-and-firewalling>`_.


Stopping and Starting VMs
-------------------------

Once a VM instance is created, you can stop, restart, or delete it as
needed. In the OOTC UI, click Instances, select the VM, and use
the Stop, Start, Reboot, and Destroy buttons.

A stop will attempt to gracefully shut down the operating system, via 
an ACPI 'stop' command which is similar to pressing the soft power switch
on a physical server. If the operating system cannot be stopped, it will
be forcefully terminated. This has the same effect as pulling out the power
cord from a physical machine.

A reboot should not be considered as a stop followed by a start. In OOTC,
a start command reconfigures the virtual machine to the stored parameters in 
OOTC's database.  The reboot process does not do this.


Deleting VMs
-------------------------

A running virtual machine
will be abruptly stopped before it is deleted. 

To delete a virtual machine:

#. Log in to the OOTC UI.

#. In the left navigation, click Instances.

#. Choose the VM that you want to delete.

#. Click the Destroy Instance button. |Destroyinstance.png|

#. Optionally both expunging and the deletion of any attached volumes can be enabled.

When the VM and its rooot disk
have been deleted, the VM is said to have been expunged.

Once a virtual machine delete, all the
resources used by the virtual machine will be reclaimed by the system,
This includes the virtual machine’s IP address.  

Managing Virtual Machines
=========================

Changing the VM Name, OS, or Group
-------------------------------------

After a VM is created, you can modify the display name, operating
system, and the group it belongs to.

To access a VM through the OOTC UI:

#. Log in to the OOTC UI.

#. In the left navigation, click Instances.

#. Select the VM that you want to modify.

#. Click the Stop button to stop the VM. |StopButton.png|

#. Click Edit. |EditButton.png|

#. Make the desired changes to the following:

#. **Display name**: Enter a new display name if you want to change the
   name of the VM.

#. **OS Type**: Select the desired operating system.

#. **Group**: Enter the group name for the VM.

#. Click Apply.


.. _cpu-and-memory-scaling:

CPU and Memory Scaling for Running VMs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is not always possible to accurately predict the CPU and RAM
requirements when you first deploy a VM. You might need to increase
these resources at any time during the life of a VM. You can dynamically
modify CPU and RAM levels to scale up these resources for a running VM
without incurring any downtime.

To scale CPU and memory in a running VM:

#. Log in to the OOTC UI.

#. In the left navigation, click Instances.

#. Choose the VM that you want to work with.

   If the VM can be dynamically scaled, a label "Dynamically Scalable" is displayed.

#. Click the Scale VM button. |ScaleVMButton.png|

   The Scale VM dialog box is displayed.

#. Select the offering you want to apply to the selected VM.

#. Click OK.


Limitations
~~~~~~~~~~~

-  On VMs running Linux 64-bit and Windows 7 32-bit operating systems,
   if the VM is initially assigned a RAM of less than 3 GB, it can be
   dynamically scaled up to 3 GB, but not more. This is due to a known
   issue with these operating systems, which will freeze if an attempt
   is made to dynamically scale from less than 3 GB to more than 3 GB.




Affinity Groups
~~~~~~~~~~~~~~~

By defining affinity groups and assigning VMs to them, the user 
can influence (but not dictate) which VMs should run on
separate hosts. This feature is to let users specify that VMs with the
same “host anti-affinity” type won’t be on the same host. This serves to
increase fault tolerance. If a host fails, another VM offering the same
service (for example, hosting the user's website) is still up and
running on another host.

The scope of an affinity group is per user account.


Creating a New Affinity Group
'''''''''''''''''''''''''''''

To add an affinity group:

#. Log in to the OOTC UI as an administrator or user.

#. In the left navigation bar, click Affinity Groups.

#. Click Add affinity group. In the dialog box, fill in the following
   fields:

   -  Name. Give the group a name.

   -  Description. Any desired text to tell more about the purpose of
      the group.

   -  Type. Anti-affinity indicates that the VMs in this group should
      avoid being placed on the same host with each other. Affinity indicates that 
      the VMs in this group should be placed on the same host.


Assign a New VM to an Affinity Group
''''''''''''''''''''''''''''''''''''

To assign a new VM to an affinity group:

-  Create the VM as usual, as described in `“Creating
   VMs” <virtual_machines.html#creating-vms>`_. Click on "Advanced Mode".
   Select the affinity groups, from the list.


Change Affinity Group for an Existing VM
''''''''''''''''''''''''''''''''''''''''

To assign an existing VM to an affinity group:

#. Log in to the OOTC UI as user.

#. In the left navigation bar, click Instances.

#. Click the name of the VM you want to work with.

#. Stop the VM by clicking the Stop button.

#. Click the Change Affinity button. |change-affinity-button.png|


View Members of an Affinity Group
'''''''''''''''''''''''''''''''''

To see which VMs are currently assigned to a particular affinity group:

#. In the left navigation bar, click Affinity Groups.

#. Click the name of the group you are interested in.

#. Click View Instances. The members of the group are listed.

   From here, you can click the name of any VM in the list to access all
   its details and controls.


Delete an Affinity Group
''''''''''''''''''''''''

To delete an affinity group:

#. In the left navigation bar, click Affinity Groups.

#. Click the name of the group you are interested in.

#. Click Delete.

   Any VM that is a member of the affinity group will be disassociated
   from the group. The former group members will continue to run
   normally on the current hosts, but if the VM is restarted, it will no
   longer follow the host allocation rules from its former affinity
   group.



Virtual Machine Snapshots
=========================


In addition to the existing OOTC ability to snapshot individual VM
volumes, you can take a VM snapshot to preserve all the VM's data
volumes as well as (optionally) its CPU/memory state. This is useful for
quick restore of a VM. For example, you can snapshot a VM, then make
changes such as software upgrades. If anything goes wrong, simply
restore the VM to its previous state using the previously saved VM
snapshot.

The snapshot is created using the hypervisor's native snapshot facility.
The VM snapshot includes not only the data volumes, but optionally also
whether the VM is running or turned off (CPU state) and the memory
contents. The snapshot is stored in OOTC's primary storage.

VM snapshots can have a parent/child relationship. Each successive
snapshot of the same VM is the child of the snapshot that came before
it. Each time you take an additional snapshot of the same VM, it saves
only the differences between the current state of the VM and the state
stored in the most recent previous snapshot. The previous snapshot
becomes a parent, and the new snapshot is its child. It is possible to
create a long chain of these parent/child snapshots, which amount to a
"redo" record leading from the current state of the VM back to the
original.

After VM snapshots are created, they can be tagged with a key/value pair,
like many other resources in OOTC.

Limitations on VM Snapshots
---------------------------

-  If a VM has some stored snapshots, you can't attach new volume to the
   VM or delete any existing volumes. If you change the volumes on the
   VM, it would become impossible to restore the VM snapshot which was
   created with the previous volume structure. If you want to attach a
   volume to such a VM, first delete its snapshots.

-  VM snapshots which include both data volumes and memory can't be kept
   if you change the VM's service offering. Any existing VM snapshots of
   this type will be discarded.

-  You can't make a VM snapshot at the same time as you are taking a
   volume snapshot.



Using VM Snapshots
------------------

To create a VM snapshot using the OOTC UI:

#. Log in to the OOTC UI.

#. Click Instances.

#. Click the name of the VM you want to snapshot.

#. Click the Take VM Snapshot button. |VMSnapshotButton.png|

   .. note:: 
      If a snapshot is already in progress, then clicking this button 
      will have no effect.

#. Provide a name and description. These will be displayed in the VM
   Snapshots list.

#. (For running VMs only) If you want to include the VM's memory in the
   snapshot, click the Memory checkbox. This saves the CPU and memory
   state of the virtual machine. If you don't check this box, then only
   the current state of the VM disk is saved. Checking this box makes
   the snapshot take longer.

..
   @Question: Assume Quise is not supported on Xen.

#. Click OK.

To delete a snapshot or restore a VM to the state saved in a particular
snapshot:

#. Navigate to the VM as described in the earlier steps.

#. Click View VM Snapshots.

#. In the list of snapshots, click the name of the snapshot you want to
   work with.

#. Depending on what you want to do:

   To delete the snapshot, click the Delete button. |delete-button.png|

   To revert to the snapshot, click the Revert button. |revert-vm.png|

.. note:: 
   VM snapshots are deleted automatically when a VM is destroyed. You don't 
   have to manually delete the snapshots in this case.


Using SSH Keys for Authentication
=================================

In addition to the username and password, OOTC
supports SSH keys for authentication.

Because each cloud user has their own SSH key, one cloud user cannot log
in to another cloud user's instances unless they share their SSH key
files. You can assigna one SSH Key to multiple instances.


Creating an SSH Key Pair
----------------------------------------------------

#. Log in to the OOTC UI.

#. Click Instances. In Select View click SSH Key Pairs.

#. Click Creat SSH Key Pair.

#. Fill in the following fields:

   - Name. Give a name for your new SSH Key Pair.

   - Public Key.If you have an already created key pair, copy and paste the public key.
   If you want OOTC to create new key pair, leave this blank.

#. Click OK.

#. If you did not provide the Public Key, copy download and save the private key. 
   OOTC will not store the private key, so if you loose your private key it 
   cannot be recovered.


Creating an Instance with SSH Key Pair
--------------------------------------

After creating a SSH Key Pair, you can create new VMs with it.
When creating the VM, select the key pair under SSH KeyPairs.


Logging In Using the SSH Keypair
---------------------------------

To test your SSH key generation is successful, check whether you can log
in to the cloud setup.

For example, from a Linux OS, run:

.. parsed-literal::

   ssh -i ~/.ssh/keypair-doc <ip address>

The -i parameter tells the ssh client to use a ssh key found at
~/.ssh/keypair-doc.


.. include:: virtual_machines/user-data.rst


..
   @Question: Assume GPU is not supported.