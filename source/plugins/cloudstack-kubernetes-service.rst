.. 
   "Option One Technologies Cloud" (OOTC) documentation.

OOTC Kubernetes Service
==============================

Kubernetes clusters
--------------------

The Kubernetes service provides the functionality of running and managing Kubernetes clusters. Highly available, scalable Kubernetes clusters can be created to run containerized deployments without having to set up Kubernetes on each container node manually. The service will automatically provision the desired number of virtual machines as per cluster size using the binaries from the given Kubernetes version. Additionally, the service provides the functionality to upgrade and scale clusters. Running clusters can be upgraded to a newer minor or patch Kubernetes version at a time. Running clusters can also be scaled for the number of worker nodes up and down and for the service offering used by each node.


Managing Kubernetes clusters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users can create, stop, start, scale, upgrade and delete Kubernetes clusters from the OOTC UI.

Creating a new Kubernetes cluster
##################################

To create a new Kubernetes cluster:

#. Log in to the OOTC UI.

#. In the left navigation bar, click on compute icon |compute-icon.png|, and select Kubernetes from the menu.

#. Click on Create Kubernetes Cluster.

#. In the dialog box fill in the fields:

   - Name. Give a name for the new Kubernetes cluster.

   - Description. Give a brief description about the new Kubernetes cluster.

   - Zone. Select the zone you want to deploy the Kubernetes cluster.

   - Kubernetes version. Select the Kubernetes version from the drop-down list.

   - Compute offering. Select the compute offering for the virtual machines (nodes) in the cluster.

   - Node root disk size. Specify the root disk size of the virtual machines, in GB.

   - Network. Select the network for the Kubernetes cluster.

   - Cluster size. Specify the number of virtual machines that you need to create in the cluster.

   - SSH Key Pair. Name of the ssh key pair used to login to the virtual machines.

#. Click on the OK button to create the cluster.

On successful creation, the new cluster will be automatically started and will show up in Running state. 

.. note::
   - A minimum of 2 cores of CPU and 2GB of RAM is required for nodes in the cluster. Therefore, please ensure that you provde a compute offering that satisfy this minimum requirement.

Listing Kubernetes clusters
############################

To list the Kubernetes clusters:

#. Log in to the OOTC UI.

#. In the left navigation bar, click on compute icon |compute-icon.png|, and select Kubernetes from the menu.

The Kubernets clusters will be shown in the UI.

Stopping Kubernetes cluster
############################

To stop a Kubernetes cluster:

#. Log in to the OOTC UI.

#. In the left navigation bar, click on compute icon |compute-icon.png|, and select Kubernetes from the menu.

#. Select the Kubernetes cluster you want to stop.

#. Click on the Stop Cluster button. |stop-cluster.png|


Starting a stopped Kubernetes cluster
######################################

To start a Kubernetes cluster in stopped state:

#. Log in to the OOTC UI.

#. In the left navigation bar, click on compute icon |compute-icon.png|, and select Kubernetes from the menu.

#. Select the Kubernetes cluster you want to start.

#. Click on the Start Cluster button. |start-cluster.png|


Scaling Kubernetes cluster
###########################

..
   @Todo: To be completed, after creating a Kubernetes cluster

Upgrading Kubernetes cluster
#############################

..
   @Todo: To be completed, after creating a Kubernetes cluster

.. note:: Kubernetes can be upgraded from one MINOR version to the next MINOR version, or between PATCH versions of the same MINOR. That is, you cannot skip MINOR versions when you upgrade. For example, you can upgrade from 1.y to 1.y+1, but not from 1.y to 1.y+2. Therefore, service can upgrade running clusters in the similar manner only.

Deleting Kubernetes cluster
############################

To delete a Kubernetes cluster:

#. Log in to the OOTC UI.

#. In the left navigation bar, click on compute icon |compute-icon.png|, and select Kubernetes from the menu.

#. Select the Kubernetes cluster you want to start.

#. Click on the Delete Cluster button. |delete-cluster.png|

Working with Kubernetes cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|cks-cluster-details-tab.png|

Once a Kubernetes cluster is created successfully and it is running state, it can be accessed using kubectl tool using cluster’s kubeconfig file. The web dashboard can be accessed by running local proxy using kubectl. Deployments in the cluster can be done using kubectl or web dashboard. More about deployment in Kubernetes here: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

..
   @Todo: To be updated, after creating a Kubernetes cluster


Accessing Kubernetes cluster
#############################

Instructions for accessing a running cluster will be shown in Access tab in the UI.

The service provides functionality to access kubeconfig file for a running Kubernetes cluster. This can be done using the UI or API. Action icon is shown in cluster detail UI to download kubeconfig file. UI will show download links for kubectl tool for different OS based on the cluster version.

getKubernetesClusterConfig API can be used to retrieve kubeconfig file data for a cluster. It takes id of the cluster as the input parameter.

Kubernetes cluster web dashboard
#################################

The service while creating a cluster automatically deploys dashboard for the cluster. More details about Kubernetes dashboard here: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

Instructions for accessing the dashboard for a running cluster will be shown in the Access tab in the UI. Essentially, the user needs to run a local proxy first using kubectl and kubecofig file for the cluster to access the dashboard. For secure login, the service doesn’t enable kubeconfig based login for the dashboard. Token-based access is enabled and kubectl can be used to access service account secret token.

|cks-cluster-access-tab.png|

The following command can be used, while passing the correct path to kubeconfig file, to run proxy:

.. parsed-literal::

   # kubectl --kubeconfig /custom/path/kube.config proxy

Once the proxy is running user can open the following URL in the browser to open the dashboard,

.. parsed-literal::

   http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

|cks-cluster-dashboard.png|

Token for dashboard login can be retrieved using following command

.. parsed-literal::

   # kubectl --kubeconfig /custom/path/kube.config describe secret $(kubectl --kubeconfig /custom/path/kube.config get secrets -n kubernetes-dashboard | grep kubernetes-dashboard-token | awk '{print $1}') -n kubernetes-dashboard

..
   @Todo: To be completed, after creating a Kubernetes cluster


.. |cks-add-version-form.png| image:: /_static/images/cks-add-version-form.png
   :alt: Add Kubernetes Supported Version form.
.. |cks-cluster-access-tab.png| image:: /_static/images/cks-cluster-access-tab.png
   :alt: Kubernetes cluster access tab.
.. |cks-cluster-dashboard.png| image:: /_static/images/cks-cluster-dashboard.png
   :alt: Kubernetes cluster dashboard.
.. |cks-cluster-details-tab.png| image:: /_static/images/cks-cluster-details-tab.png
   :alt: Kubernetes details tab.
.. |cks-clusters.png| image:: /_static/images/cks-clusters.png
   :alt: Kubernetes clusters list.
.. |cks-create-cluster-form.png| image:: /_static/images/cks-create-cluster-form.png
   :alt: Create Kubernetes Cluster form.
.. |cks-delete-action.png| image:: /_static/images/cks-delete-action.png
   :alt: Delete action icon.
.. |cks-kube-config-action.png| image:: /_static/images/cks-kube-config-action.png
   :alt: Download kube-config action icon.
.. |cks-scale-action.png| image:: /_static/images/cks-scale-action.png
   :alt: Scale action icon.
.. |cks-scale-cluster-form.png| image:: /_static/images/cks-scale-cluster-form.png
   :alt: Scale Kubernetes Cluster form.
.. |cks-start-action.png| image:: /_static/images/cks-start-action.png
   :alt: Start action icon.
.. |cks-stop-action.png| image:: /_static/images/cks-stop-action.png
   :alt: Stop action icon.
.. |cks-upgrade-action.png| image:: /_static/images/cks-upgrade-action.png
   :alt: Upgrade action icon.
.. |cks-upgrade-cluster-form.png| image:: /_static/images/cks-upgrade-cluster-form.png
   :alt: Upgrade Kubernetes Cluster form.
.. |cks-versions.png| image:: /_static/images/cks-versions.png
   :alt: Supported Kubernetes versions list.
