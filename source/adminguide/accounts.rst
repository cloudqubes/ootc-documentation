.. 
   "Option One Technologies Cloud" (OOTC) documentation.
 

Roles, Accounts, Users, and Domains
-----------------------------------

Roles
~~~~~

A role represents a set of allowed functions. All OOTC accounts have a
role attached to them that enforce access rules on them to be allowed or
disallowed to make an API request. Typically there are four default roles:
root admin, resource admin, domain admin and user.


Accounts
~~~~~~~~

An account typically represents a customer of the service provider or a
department in a large organization. Multiple users can exist in an
account.


Domains
~~~~~~~

Accounts are grouped by domains. Domains usually contain multiple
accounts that have some logical relationship to each other and a set of
delegated administrators with some authority over the domain and its
subdomains. For example, a service provider with several resellers could
create a domain for each reseller.

Beside the Root Administrator type of account (available in the root domain only), two different types
of accounts can be created for each domain:  Domain Administrator and User.


Users
~~~~~

Users are like aliases in the account. Users in the same account are not
isolated from each other, but they are isolated from users in other
accounts. Most installations need not surface the notion of users; they
just have one user per account. The same user cannot belong to multiple
accounts.

Username is unique in a domain across accounts in that domain. The same
username can exist in other domains, including sub-domains. Domain name
can repeat only if the full pathname from root is unique. For example,
you can create root/d1, as well as root/foo/d1, and root/sales/d1.

Resource Ownership
~~~~~~~~~~~~~~~~~~

Resources belong to the account, not individual users in that account.
For example, billing, resource limits, and so on are maintained by the
account, not the users. A user can operate on any resource in the
account provided the user has privileges for that operation. The
privileges are determined by the role. 

