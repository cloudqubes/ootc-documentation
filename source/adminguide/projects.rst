.. 
   "Option One Technologies Cloud" (OOTC) documentation.


Overview of Projects
--------------------

Projects are used to organize people and resources. You can use projects
to group virtual resources such as VMs, snapshots,templates, data disks, 
and IP addresses, so users within the same project can share resources among them.
OOTC tracks resource usage per project as well as per user, so the usage can be billed to
either a user account or a project. For example, all members of your QA department might be assigned
to one project, so the you can track the resources used in testing
while the project members can more easily isolate their efforts from
other users.

Once
you have created a project, you become that project’s administrator, and
you can add others within your domain to the project. OOTC can be
set up to either add people directly to a project, or to send an
invitation which the recipient must accept. Project members can view
and manage all virtual resources created by anyone in the project
(for example, share VMs). A user can be a member of any number of projects
and can switch views in the OOTC UI to show only project-related information,
such as project VMs, fellow project members, project-related alerts, and so on.

It is possible for a project to have
multiple project administrators and to add/invite specific users of
an account to a project in addition to adding accounts. By means of
Project Roles associated with a user or an account of the project,
it is possible to restrict access of users in a project, i.e., in
addition to account-level roles, one can further restrict access to
operations (or APIs) by associating a project-level role to the
user or account. However, if an account has already been added, one will not
be able to associate a role to a specific user of that account.

**NOTE:** Project Roles work over Account level Roles. If a user/account is
added to a project without a project role, it would imply that the
user / account added will have access to all APIs that are made available
by the Account level role. If there are no specific deny rules in the
project role, it would again fallback onto the account-level role to decide
whether the user has permissions to perform a specific action. It is also to be
noted that Project roles are restrictive in nature, i.e., to say that, one may
not allow a user to perform an operation that is NOT allowed at the Account level.
Even if a rule is added at the project level, allowing such an action, it will not
have any effect as the action will be prohibited by the Account Role.


The project administrator can promote or demote a user in the project.
The project administrator can also add more members, remove members
from the project, set new resource limits and
delete the project. When the administrator removes a member from the
project, resources created by that user, such as VM instances, remain
with the project. This brings us to the subject of resource ownership
and which resources can be used by a project.

Resources created within a project are owned by the project, not by any
particular OOTC account, and they can be used only within the
project. A user who belongs to one or more projects can still create
resources outside of those projects, and those resources belong to the
user’s account; they will not be counted against the project’s usage or
resource limits. You can create project-level networks to isolate
traffic within the project and provide network services such as port
forwarding, load balancing, VPN, and static NAT. A project can also make
use of certain types of resources from outside the project, if those
resources are shared. For example, a shared network or public template
is available to any project in the domain. A project can get access to a
private template if the template’s owner will grant permission. A
project can use any service offering or disk offering available in its
domain; however, you can not create private service and disk offerings
at the project level.


Configuring Projects
--------------------




Creating a New Project
----------------------


#. Log to the OOTC UI.

#. In the left navigation, click Projects.

#. Click New Project.

#. Give the project a name and description for display to users, then
   click Create Project.

#. Click OK.


Adding Members to a Project
---------------------------

New members can be added to a project by the Admin user of the project.


#. Log in to the OOTC UI.

#. In the left navigation, click Projects.

#. Click the name of the project you want to work with.

#. Click on the `Add Account to Project` button. This will have 2 tabs, one to add account to the project and the other to add a user to the project. Here, we can specify the:

      - account or user and/or email id of the user to be invited,
      - (Optional) the Role i.e, Admin or Regular that the user is to be added as, defualts to Regular role,
      - (Optional) the Project role specifying the list of APIs the user is allowed/ denied access to

#. You can add only people who have an account in this cloud and within the same domain as the project.



Suspending or Deleting a Project
--------------------------------

When a project is suspended, it retains the resources it owns, but they
can no longer be used. No new resources or members can be added to a
suspended project.

When a project is deleted, its resources are destroyed, and member
accounts are removed from the project. The project’s status is shown as
Disabled pending final deletion.

A project can be suspended or deleted by the project administrator.


#. Log in to the OOTC UI.

#. In the left navigation, click Projects.

#. Click the name of the project.

#. Click one of the buttons:

   To delete, use |Removes a project|

   To suspend, use |Suspends a project|


Using the Project View
----------------------

If you are a member of a project, you can use OOTC’s project view
to see project members, resources consumed, and more. The project view
shows only information related to one project. It is a useful way to
filter out other information so you can concentrate on a project status
and resources.

#. Log in to the OOTC UI.

#. Click Project View.

#. The project dashboard appears, showing the project’s VMs, volumes,
   users, events, network settings, and more. From the dashboard, you
   can:

   -  Click the Accounts tab to view and manage project members. If you
      are the project administrator, you can add new members, remove
      members, or change the role of a member from user to admin or vice versa.


.. |Edits Parameters| image:: /_static/images/edit-icon.png
.. |Searches projects| image:: /_static/images/search-button.png
.. |Removes a project| image:: /_static/images/delete-button.png
.. |Suspends a project| image:: /_static/images/suspend-icon.png
