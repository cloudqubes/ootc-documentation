.. 
   "Option One Technologies Cloud" (OOTC) documentation.

User-Data and Meta-Data
-----------------------

When creating a new VM in the OOTC UI, you can specify a user-data string.
This string will be made available to the VM, so you can use it to pass configuration
parameters to the VM.

This user data can be accesed from the VM via cloud-init or an HTTP API.

Using HTTP API
~~~~~~~~~~~~~~~~
User-data is available from the URL http://data-server./latest/user-data and can be fetched via 
curl or other HTTP client.

..
   @question: Assume above is supported in OOTC

Using cloud-init
~~~~~~~~~~~~~~~~

`cloud-init <https://cloudinit.readthedocs.org/en/latest>`_ can be used to access
and interpret user-data inside virtual machines. If you install cloud-init into your
VM templates, it will allow you to store SSH keys and user passwords on each new
VM deployment automatically (:ref:`adding-password-management-to-templates` and `using ssh keys <virtual_machines.html#using-ssh-keys-for-authentication>`_).

#. Install cloud-init package into a VM template:

   .. code:: bash

      # yum install cloud-init
        or
      $ sudo apt-get install cloud-init



Custom user-data example
~~~~~~~~~~~~~~~~~~~~~~~~

This example uses cloud-init to automatically update all OS packages on the first launch.

#. Create user-data, wrapped into a multi-part MIME message and encoded in base64:

.. code:: bash

   base64 <<EOF
   Content-Type: multipart/mixed; boundary="//"
   MIME-Version: 1.0
   
   --//
   Content-Type: text/cloud-config; charset="us-ascii"
   MIME-Version: 1.0
   Content-Transfer-Encoding: 7bit
   Content-Disposition: attachment; filename="cloud-config.txt"
   
   #cloud-config
   
   # Upgrade the instance on first boot
   # (ie run apt-get upgrade)
   #
   # Default: false
   # Aliases: apt_upgrade
   package_upgrade: true
   EOF

Creating VM with this user-data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the OOTC UI.

#. In the left navigation bar, click Instances in the Compute menu. |compute-icon.png|

#. Click Add Instance.

#. Provide the other parameters as required.

#. Click on "Show advanced settings". Copy and paste the user-data in to the 
"Userdata" field.

#. Launch the VM.

.. |compute-icon.png| image:: /_static/images/compute-icon.png
   :alt: Compute.