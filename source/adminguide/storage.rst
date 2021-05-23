.. 
   "Option One Technologies Cloud" (OOTC) documentation.

Storage Overview
----------------

OOTC has two type of storage volumes; Root volumes and data volumes.
Root volumes are created automatically when a virtual machine is
created, and root volumes are deleted when the VM is destroyed. Data volumes
can be created and dynamically attached to VMs. But, data volumes are not
deleted when VMs are destroyed.

Working With Volumes
--------------------

OOTC defines a volume as a unit of storage available to a guest
VM. Volumes are either root disks or data disks. The root disk has "/"
in the file system and is usually the boot device. Data disks provide
for additional storage, for example: "/opt" or "D:". Every VM has
a root disk. VMs can also optionally have one or more data disks. 

Creating a New Volume
~~~~~~~~~~~~~~~~~~~~~



To Create a New Volume
^^^^^^^^^^^^^^^^^^^^^^

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click Create Volume, provide the following
   details, and click OK.

   -  Name. Give the volume a unique name so you can find it later.

   -  Availability Zone. Where do you want the storage to reside? This
      should be close to the VM that will use the volume.

   -  Disk Offering. Choose the characteristics of the storage.

   The new volume appears in the list of volumes with the state
   “Allocated.” The volume data is stored in OOTC, but the volume
   is not yet ready for use

#. To start using the volume, continue to Attaching a Volume


Uploading an Existing Volume to a Virtual Machine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Existing data can be made accessible to a virtual machine. This is
called uploading a volume to the VM. For example, this is useful to
upload data from a local file system and attach it to a VM. 

The upload is performed using HTTP. The uploaded volume is placed in the
zone's secondary storage

To upload a volume:

#. (Optional) Create an MD5 hash (checksum) of the disk image file that
   you are going to upload. After uploading the data disk, OOTC
   will use this value to verify that no data corruption has occurred.

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click Upload Volume. |upload-volume.png|

#. Provide the following:

   -  Name and Description. Any desired name and a brief description
      that can be shown in the UI.

   -  Availability Zone. Choose the zone where you want to store the
      volume. VMs running on hosts in this zone can attach the volume.

   -  Format. Choose one of the following to indicate the disk image
      format of the volume.

   -  URL. The secure HTTP or HTTPS URL that OOTC can use to
      access your disk. The type of file at the URL must match the value
      chosen in Format. For example, if Format is VHD, the URL might
      look like the following:

      ``http://yourFileServerIP/userdata/myDataDisk.vhd``

   -  MD5 checksum. (Optional) Use the hash that you created in step 1.

#. Wait until the status of the volume shows that the upload is
   complete.


Attaching a Volume
~~~~~~~~~~~~~~~~~~

You can attach a volume to a guest VM to provide extra disk storage.
Attach a volume when you first create a new volume, when you are moving
an existing volume from one VM to another, or after you have migrated a
volume from one storage pool to another.

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click the volume name in the Volumes list, then click the Attach Disk
   button |AttachDiskButton.png|

#. In the Instance popup, choose the VM to which you want to attach the
   volume.

#. When the volume has been attached, you should be able to see it in 
   volumes tab in the instance view.


Detaching and Moving Volumes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A volume can be detached from a guest VM and attached to another guest.

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|
   Alternatively, you can go to the VM instance view, and click Volumes tab.

#. Click the name of the volume you want to detach, then click the
   Detach Disk button. |DetachDiskButton.png|

#. To move the volume to another VM, follow the steps in
   `“Attaching a Volume” <#attaching-a-volume>`_.


Resizing Volumes
~~~~~~~~~~~~~~~~

OOTC provides the ability to resize voluems.

Before you try to resize a volume, it is recommended to make a backup
of your data to eliminate any risk of data loss.

When a volume is shrunk, the disk associated with it is simply
truncated, and doing so would put its content at risk of data loss.
Therefore, resize any partitions or file systems before you shrink a
data disk so that all the data is moved off from that disk.

To resize a volume:

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Select the volume name in the Volumes list, then click the Resize
   Volume button |resize-volume-icon.png|

#. In the Resize Volume pop-up, choose desired characteristics for the
   storage.

   |resize-volume.png|

   #. If you select Custom Disk, specify a custom size.

   #. Click Shrink OK to confirm that you are reducing the size of a
      volume.

      This parameter protects against inadvertent shrinking of a disk,
      which might lead to the risk of data loss. You must sign off that
      you know what you are doing.

#. Click OK.



Volume Deletion
~~~~~~~~~~~~~~~

The deletion of a volume does not delete the snapshots that have been
created from the volume

When a VM is destroyed, data volumes that are attached to the VM
are not deleted. But, the root volume of the VM is deleted.

To delete a volume:

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|
   Make sure the volume is not attached to a VM.

#. Select the volume name in the Volumes list, then click the Destroy
   button |destroy-icon.png|


Working with Volume Snapshots
-----------------------------

OOTC supports snapshots of disk volumes. Snapshots are a
point-in-time capture of virtual machine disks. Memory and CPU states
are not captured. Snapshots can be created from either root or data volumes. 

You can create new volumes from the snapshot for
recovery of particular files. Such voluems created from snapshots
may be attached to a VM like any other data volume. But, you cannot boot new 
VMs from those volumes. 

You can also create templates from snapshots. These templates can be used to 
create new VMs.

How to Snapshot a Volume
~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click the name of the volume you want to snapshot.

#. Click the Snapshot button. |SnapshotButton.png|

..
   @Question: What is the Async Backup check in Take Snapshot dialog box?


Automatic Snapshot Creation and Retention
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


You can set up a recurring snapshot policy to automatically create
multiple snapshots of a disk at regular intervals. Snapshots can be
created on an hourly, daily, weekly, or monthly interval. One snapshot
policy can be set up per disk volume. For example, you can set up a
daily snapshot at 02:30.

With each snapshot schedule, you can also specify the number of
scheduled snapshots to be retained. Older snapshots that exceed the
retention limit are automatically deleted. 

To enable automatic snapshot creation:

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click the name of the volume you want to snapshot.

#. Click the Recurring Snapshots button. |recurring-snapshots-button.png|

#. Fill in the fields.

   - Interval Type. Select the frequency of snapshot creation.

   - Time. Give the time you want to create the snapshot.

   - Keep. Give the number of snapshots you want to retain.

   - Timezone. Specify your timezone.

#. Click OK. In the same dialog box, click on Scheduled Snapshots to view the snapshot creation schedule.

To disable automatic snapshot creation:

#. Log in to the OOTC UI.

#. In the left navigation bar, click Volumes in Storage menu. |storage-icon.png|

#. Click the name of the volume you want to snapshot.

#. Click the Recurring Snapshots button. |recurring-snapshots-button.png|

#. Click on Scheduled Snapshots to view the snapshot creation schedule.

#. On the schedule you want to delete, click on the Delete button. |delete-button.png|



Volume Status
~~~~~~~~~~~~~

When a snapshot operation is triggered by means of a recurring snapshot
policy, a snapshot is skipped if a volume has remained inactive since
its last snapshot was taken. A volume is considered to be inactive if it
is either detached or attached to a VM that is not running. OOTC
ensures that at least one snapshot is taken since the volume last became
inactive.

When a snapshot is taken manually, a snapshot is always created
regardless of whether a volume has been active or not.


Snapshot Restore
~~~~~~~~~~~~~~~~

There are two paths to restoring snapshots. You can create a volume
from the snapshot. The volume can then be mounted to a VM and files
recovered as needed. Alternatively, a template may be created from the
snapshot of a root disk. You must then boot a VM from this template
to effect recovery of the root disk.



.. |AttachDiskButton.png| image:: /_static/images/attach-disk-icon.png
   :alt: Attach Disk Button.
.. |resize-volume-icon.png| image:: /_static/images/resize-volume-icon.png
   :alt: button to display the resize volume option.
.. |resize-volume.png| image:: /_static/images/resize-volume.png
   :alt: option to resize a volume.
.. |SnapshotButton.png| image:: /_static/images/SnapshotButton.png
   :alt: Snapshot Button.
.. |DetachDiskButton.png| image:: /_static/images/detach-disk-icon.png
   :alt: Detach Disk Button.
.. |Migrateinstance.png| image:: /_static/images/migrate-instance.png
   :alt: button to migrate a volume.
.. |volume-from-snap.PNG| image:: /_static/images/volume-from-snap.PNG
   :alt: Offering is needed when creating a volume from the ROOT volume snapshot.
