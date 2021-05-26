.. 
   "Option One Technologies Cloud" (OOTC) documentation.

Working With Templates
=======================

A template is a reusable configuration for virtual machines. When launching 
VMs, you can choose from a list of templates in OOTC.

Specifically, a template is a virtual disk image that includes one of a
variety of operating systems, optional additional software such as
office applications, and settings such as access control to determine
who can use the template. 

OOTC has some default templates, and you can create addtitional templates
according to your requirements.

Creating Templates: Overview
----------------------------

The typical sequence of creating a template:

#. Launch a VM instance that has the operating system you want. Make any
   other desired configuration changes to the VM.

#. Stop the VM.

#. Convert the volume into a template.

There are other ways to add templates to OOTC. For example, you
can take a snapshot of the VM's volume and create a template from the
snapshot, or import a VHD from another system into OOTC.

The various techniques for creating templates are described in the next
few sections.



The Default Template
--------------------

OOTC includes a CentOS template. This template is downloaded by
the Secondary Storage VM after the primary and secondary storage are
configured. You can use this template in your production deployment or
you can delete it and use custom templates.

The password of the root user in default template is "password".

..
   @Question: There are several templates. Need to confirm whether this is correct for all of them.


The default template includes the standard iptables rules, which will
block most access to the template excluding ssh.

.. code:: bash

   # iptables --list
   Chain INPUT (policy ACCEPT)
   target     prot opt source               destination
   RH-Firewall-1-INPUT  all  --  anywhere             anywhere

   Chain FORWARD (policy ACCEPT)
   target     prot opt source               destination
   RH-Firewall-1-INPUT  all  --  anywhere             anywhere

   Chain OUTPUT (policy ACCEPT)
   target     prot opt source               destination

   Chain RH-Firewall-1-INPUT (2 references)
   target     prot opt source               destination
   ACCEPT     all  --  anywhere             anywhere
   ACCEPT     icmp --  anywhere        anywhere       icmp any
   ACCEPT     esp  --  anywhere        anywhere
   ACCEPT     ah   --  anywhere        anywhere
   ACCEPT     udp  --  anywhere        224.0.0.251    udp dpt:mdns
   ACCEPT     udp  --  anywhere        anywhere       udp dpt:ipp
   ACCEPT     tcp  --  anywhere        anywhere       tcp dpt:ipp
   ACCEPT     all  --  anywhere        anywhere       state RELATED,ESTABLISHED
   ACCEPT     tcp  --  anywhere        anywhere       state NEW tcp dpt:ssh
   REJECT     all  --  anywhere        anywhere       reject-with icmp-host-


..
   @Question: Need to confirm whether this is applicable for all the templates.

Creating a Template from an Existing Virtual Machine
----------------------------------------------------

Once you have at least one VM set up in the way you want, you can use it
as the prototype for other VMs.

#. Create and start a virtual machine using any of the techniques given
   in `“Creating VMs” <virtual_machines.html#creating-vms>`_.

#. Make any desired configuration changes on the running VM, then stop the VM.

#. Wait for the VM to stop. When the status shows Stopped, go to the
   next step.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. From the list of volumes, click on the volume belonging to the VM.

#. Click Create Template |create-template-icon.png| and provide the following:

   -  **Name**. These will be shown in the UI, so
      choose something descriptive.

   - **Description**. Give a meaningful description here.

   -  **OS Type**. This helps OOTC and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following.

      -  If the operating system of the stopped VM is listed, choose it.

      -  If the OS type of the stopped VM is not listed, choose Other.

      -  If you want to boot from this template in PV mode, choose Other
         PV (32-bit) or Other PV (64-bit). This choice is available only
         for XenServere:

         .. note:: 
            Generally you should not choose an older version of the OS 
            than the version in the image. For example, choosing CentOS 
            5.4 to support a CentOS 6.2 image will in general not work. 
            In those cases you should choose Other.


   -  **Public**. Choose Yes to make this template accessible to all
      users of this OOTC installation. The template will appear in
      the Community Templates list.

   -  **Password Enabled**. Choose Yes if your template has the
      OOTC password change script installed. See 
      :ref:`adding-password-management-to-templates`.

#. Click Add.

The new template will be visible in the Templates section when the
template creation process has been completed. The template is then
available when creating a new VM.

Creating a Template from a Snapshot
-----------------------------------

If you do not want to stop the VM in order to use the Create Template
menu item (as described in `“Creating a Template from an Existing 
Virtual Machine” <#creating-a-template-from-an-existing-virtual-machine>`_), 
you can create a template directly from any snapshot through the 
OOTC UI.


Uploading Templates from a remote HTTP server
---------------------------------------------

Templates are uploaded based on a URL. HTTP is the supported access
protocol. Templates are frequently large files. You can optionally gzip
them to decrease upload times.

To upload a template:

#. In the left navigation bar, click Templates in Packages menu. |package-icon.png|

..
   @Question: What would be the appropriate name for this menu icon in the navigation bar. I used "Packages". 

#. Click Register Template from URL.

#. Provide the following:

   -  **URL**. OOTC will download the template from the
      specified URL, such as ``http://my.web.server/filename.vhd.gz``.

   -  **Name**. Give a name for the new template.

   -  **Description**. Give a meaningful description for the new template.

   -  **Zone**. Choose the zone where you want the template to be
      available, or All Zones to make it available throughout
      OOTC.

   -  **OS Type**: This helps OOTC and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following:

      -  If the operating system of the stopped VM is listed, choose it.

      -  If the OS type of the stopped VM is not listed, choose Other.

         .. note:: 
            You should not choose an older version of the OS than the 
            version in the image. For example, choosing CentOS 5.4 to 
            support a CentOS 6.2 image will in general not work. In 
            those cases you should choose Other.

         .. note::
            Since version 4.15.1, VMware templates do not allow users or administrators
            selecting an OS Type when registering a template if the option 'Read VM settings from OVA' is selected. In this case, the OS Type is
            obtained from the template after it is registered.

   -  **Hypervisor**: The supported hypervisors are listed. Select the
      desired one.

..
   @Question: Shoudn't we remove the hypervisor from the UI and docs.

   -  **Format**. The format of the template upload file, such as VHD or
      OVA.

   -  **Password Enabled**. Choose Yes if your template has the
      OOTC password change script installed. 
      See :ref:`adding-password-management-to-templates`.

   -  **Extractable**. Choose Yes if the template is available for
      extraction. If this option is selected, end users can download a
      full image of a template.

   -  **Public**. Choose Yes to make this template accessible to all
      users of this OOTC installation. The template will appear in
      the Community Templates list. See `“Private and
      Public Templates” <#private-and-public-templates>`_.

   -  **Featured**. Choose Yes if you would like this template to be
      more prominent for users to select. The template will appear in
      the Featured Templates list. Only an administrator can make a
      template Featured.
      
Note that uploading multi-disk templates is also supported.


Uploading Templates and ISOs from a local computer
-------------------------------------------

It's also possible to upload an already prepared template or an ISO from your local computer.
The steps are similar as when Uploading a template/ISO from a remote HTTP server, except that you need to choose a local template/ISO file from your PC.

Example GUI dialog of uploading Template/ISO from local (browser) is given below:

|template-upload-from-local.PNG|

|upload-iso-from-local.png|

Note that uploading multi-disk templates is also supported.


Deleting Templates
------------------

Templates may be deleted. In general, when a template spans multiple
Zones, only the copy that is selected for deletion will be deleted; the
same template in other Zones will not be deleted. The provided CentOS
template is an exception to this. If the provided CentOS template is
deleted, it will be deleted from all Zones.

When templates are deleted, the VMs instantiated from them will continue
to run. However, new VMs cannot be created based on the deleted
template.

Working with ISOs
===================

OOTC supports ISOs and their attachment to guest VMs. An ISO is a
read-only file that has an ISO/CD-ROM style file system. Users can
upload their own ISOs and mount them on their guest VMs.

ISOs are uploaded based on a URL. HTTP is the supported protocol. Once
the ISO is available via HTTP specify an upload URL such as
http://my.web.server/filename.iso.


ISO images may be stored in the system and made available with a privacy
level similar to templates. ISO images are classified as either bootable
or not bootable. A bootable ISO image is one that contains an OS image.
OOTC allows a user to boot a guest VM off of an ISO image. Users
can also attach ISO images to guest VMs. For example, this enables
installing PV drivers into Windows.

Adding an ISO
---------------

To add an ISO:

#. Log in to the OOTC UI.

#. In the left navigation bar, click ISOs in Packages menu. |package-icon.png|

#. Click Add ISO.

#. In the Add ISO screen, provide the following:

   -  **URL**: The URL that hosts the ISO image.

   -  **Name**: Short name for the ISO image. For example, CentOS 6.2
      64-bit.

   -  **Description**: Display test for the ISO image. For example,
      CentOS 6.2 64-bit.

   -  **Zone**: Choose the zone where you want the ISO to be available,
      or All Zones to make it available throughout OOTC.

   -  **Bootable**: Whether or not a guest could boot off this ISO
      image. For example, a CentOS ISO is bootable, a Microsoft Office
      ISO is not bootable.

   -  **OS Type**: This helps OOTC and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following.

      -  If the operating system of your desired ISO image is listed,
         choose it.

      -  If the OS Type of the ISO is not listed or if the ISO is not
         bootable, choose Other.

      .. note:: 
         It is not recommended to choose an older version of the OS than 
         the version in the image. For example, choosing CentOS 5.4 to 
         support a CentOS 6.2 image will usually not work. In these 
         cases, choose Other.

   -  **Extractable**: Choose Yes if the ISO should be available for
      extraction.

   -  **Public**: Choose Yes if this ISO should be available to other
      users.

   -  **Featured**: Choose Yes if you would like this ISO to be more
      prominent for users to select. The ISO will appear in the Featured
      ISOs list. Only an administrator can make an ISO Featured.

#. Click OK.

   The Management Server will download the ISO. Depending on the size of
   the ISO, this may take a long time. The ISO status column will
   display Ready once it has been successfully downloaded into secondary
   storage. Clicking Refresh updates the download percentage.

#. **Important**: Wait for the ISO to finish downloading. If you move on
   to the next task and try to use the ISO right away, it will appear to
   fail. The entire ISO must be available before you can work
   with it.


Attaching an ISO to a VM
-------------------------

#. In the left navigation bar, click Instances in Compute menu. |compute-icon.png|

#. Choose the virtual machine you want to work with.

#. Click the Attach ISO button. |iso.png|

#. In the Attach ISO dialog box, select the desired ISO.

#. Click OK.



.. |sysmanager.png| image:: /_static/images/sysmanager.png
   :alt: System Image Manager
.. |software-license.png| image:: /_static/images/software-license.png
   :alt: Depicts hiding the EULA page.
.. |change-admin-password.png| image:: /_static/images/change-admin-password.png
   :alt: Depicts changing the administrator password
.. |kvm-direct-download.png| image:: /_static/images/kvm-direct-download.png
.. |upload-iso-from-local.png| image:: /_static/images/upload-iso-from-local.png
   :alt: Upload ISO from local
.. |template-upload-from-local.PNG| image:: /_static/images/template-upload-from-local.PNG
   :alt: Upload Template from local
.. |template-permissions-update-manually-1.PNG| image:: /_static/images/template-permissions-update-manually-1.PNG
   :alt: USharing template with account "user2"
.. |template-permissions-update-manually-2.PNG| image:: /_static/images/template-permissions-update-manually-2.PNG
   :alt: Revoking permissions from account "user2"
.. |template-permissions-update-1.PNG| image:: /_static/images/template-permissions-update-1.PNG
   :alt: Sharing template with just account "user8"
.. |template-permissions-update-2.PNG| image:: /_static/images/template-permissions-update-2.PNG
   :alt: Sharing template with 2 specific projects
.. |template-permissions-update-3.PNG| image:: /_static/images/template-permissions-update-3.PNG
   :alt: Revoking permissins from account "user8"
.. |template-permissions-update-4.PNG| image:: /_static/images/template-permissions-update-4.PNG
   :alt: Revoking permsissons from both projects previously added
.. |template-permissions-update-5.PNG| image:: /_static/images/template-permissions-update-5.PNG
   :alt: Reseting (removing all) permissions
.. |compute-icon.png| image:: /_static/images/compute-icon.png
   :alt: Compute
.. |package-icon.png| image:: /_static/images/package-icon.png
   :alt: Packages.
.. |iso.png| image:: /_static/images/iso.png
   :alt: Attach ISO.


