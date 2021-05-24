.. 
   "Option One Technologies Cloud" (OOTC) documentation.


Quota Plugin 
=============

Quota service, while allowing for scalability, will make sure that the cloud is
not exploited by attacks, careless use and program errors. To address this
problem, employ the quota-enforcement service that allows resource
usage within certain bounds as defined by policies and available quotas for
various entities. Quota service extends the functionality of usage server to
provide a measurement for the resources used by the accounts and domains using a
common unit referred to as cloud currency in this document. It can be configured
to ensure that your usage won’t exceed the budget allocated to accounts/domain
in cloud currency. It will let user know how much of the cloud resources he is
using. It will help the cloud admins, if they want, to ensure that a user does
not go beyond his allocated quota. Per usage cycle if an account is found to be
exceeding its quota then it is locked. Locking an account means that it will not
be able to initiate a new resource allocation request, whether it is more
storage or an additional ip. To unlock an account you need to add more credit to it.
In case you want the locking to be disabled on global or on account scope those 
provisions are also provided. 

Quota Tariff
-------------

The following table shows all quota types for which you can specify tariff.

.. cssclass:: table-striped table-bordered table-hover

+------------------+-----------------------------------+--------------------------+
| Type ID          | Type Name                         | Tariff Description       |
|                  |                                   |                          |
+==================+===================================+==========================+
| 1                | RUNNING\_VM                       | One month of running     |
|                  |                                   | Compute-Month            |
+------------------+-----------------------------------+--------------------------+
| 2                | ALLOCATED\_VM                     | One month of allocated   |
|                  |                                   | VM                       |
+------------------+-----------------------------------+--------------------------+
| 3                | IP\_ADDRESS                       | Quota for a month of     |
|                  |                                   | allocated IP             |
+------------------+-----------------------------------+--------------------------+
| 4                | NETWORK\_BYTES\_SENT              | Quota for 1GB bytes sent |
+------------------+-----------------------------------+--------------------------+
| 5                | NETWORK\_BYTES\_RECEIVED          | Quota for 1GB bytes sent |
+------------------+-----------------------------------+--------------------------+
| 6                | VOLUME                            | Quota for 1 GB of        |
|                  |                                   | Volume use for a month   |
+------------------+-----------------------------------+--------------------------+
| 7                | TEMPLATE                          | Quota for 1 GB of        |
|                  |                                   | Template use for a month |
+------------------+-----------------------------------+--------------------------+
| 8                | ISO                               | Quota for 1 GB of        |
|                  |                                   | ISO use for a month      |
+------------------+-----------------------------------+--------------------------+
| 9                | SNAPSHOT                          | Quota for 1 GB of        |
|                  |                                   | SNAPSHOT use for a month |
+------------------+-----------------------------------+--------------------------+
| 11               | LOAD\_BALANCER\_POLICY            | Quota for load balancer  |
|                  |                                   | policy month             |
+------------------+-----------------------------------+--------------------------+
| 12               | PORT\_FORWARDING\_RULE            | Quota for port forwarding|
|                  |                                   | policy month             |
+------------------+-----------------------------------+--------------------------+
| 13               | NETWORK\_OFFERING                 | Quota for network        |
|                  |                                   | Offering for a month     |
+------------------+-----------------------------------+--------------------------+
| 14               | VPN\_USERS                        | Quota for VPN usage      |
|                  |                                   | for a month              |
+------------------+-----------------------------------+--------------------------+
| 15               | CPU\_CLOCK\_RATE                  | The tariff for using     |
|                  |                                   | 1 CPU i100 MHz clock     |
+------------------+-----------------------------------+--------------------------+
| 16               | CPU\_NUMBER                       | The quota tariff for     |
|                  |                                   | using 1 virtual CPU.     |
+------------------+-----------------------------------+--------------------------+
| 17               | MEMORY                            | The quota tariff for     |
|                  |                                   | using 1MB RAM size.      |
+------------------+-----------------------------------+--------------------------+


 
Quota Statement
----------------
 
Quota statement for a period consist of the quota usage under various quota types for 
the given period from a start date to an end date.

Quota Monthly Statement
------------------------

Quota service emails the monthly quota statement for the last month at the beginning of
each month. For this service to work properly you need to ensure that the usage server
is running.
 
Quota Alert Management
-----------------------

Quota module also provides APIs to customize various email templates that are used to
alert account owners about quota going down below threshold and quota getting over.

..
   @Question: Need to update based on how OOTC is going to use quota.