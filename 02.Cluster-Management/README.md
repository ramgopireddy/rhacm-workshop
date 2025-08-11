# Exercise 2 - Managing an existing cluster using Advanced Cluster Management

In this exercise you manage the existing cluster on the Red Hat Advanced Cluster Management stack - `local-cluster`. You will attach labels to the cluster, visualize its resources and perform updates to the OpenShift Platform.


## 2.1 Import an existing cluster

1. Modify the attributes of the managed cluster in Red Hat Advanced Cluster Management -
*   **Name**: local-cluster
*   **labels**: 
    * environment=dev
    * owner=&lt;your-name>
    
In order to associate the labels with local-cluster, follow the next steps (You may use the presentation for guidance) -

*   Navigate to **Clusters** -> **local-cluster** -> **Actions** -> **Edit labels**.
*   Add the labels in the `key=value` format.

2. Log into the cluster using the **oc** cli tool.

```
<managed cluster> $ oc login -u <admin-user> -p <password> https://api.cluster.2222.sandbox.opentlc.com:6443
```

3. Make sure that all of the agent pods are up and running on the cluster.

```
<managed cluster> $ oc get pods -n open-cluster-management-agent
NAME                                READY   STATUS    RESTARTS       AGE
klusterlet-5c7cfb456b-rr2hw         1/1     Running   0              150m
klusterlet-agent-5dc6455d6d-fmxzk   1/1     Running   1 (130m ago)   150m
klusterlet-agent-5dc6455d6d-t79sf   1/1     Running   0              150m
klusterlet-agent-5dc6455d6d-w8nxp   1/1     Running   0              150m

<managed cluster> $ oc get pods -n open-cluster-management-agent-addon
NAME                                                  READY   STATUS      RESTARTS       AGE
application-manager-678f58ccd7-slqnk                  1/1     Running     1 (127m ago)   148m
cert-policy-controller-68d94554b7-j29hc               1/1     Running     0              148m
cluster-proxy-proxy-agent-7879dcbb66-ssqdv            3/3     Running     0              150m
config-policy-controller-cc65bcf9-km4gb               2/2     Running     1 (126m ago)   148m
governance-policy-framework-97d9f6578-8p8hx           2/2     Running     1 (127m ago)   148m
hypershift-addon-agent-645f49fb84-8rhw9               2/2     Running     1 (127m ago)   150m
hypershift-install-job-lrrz6-kpbcx                    0/1     Completed   0              149m
iam-policy-controller-58644657c9-td7x8                1/1     Running     0              148m
klusterlet-addon-workmgr-76966fcc95-ljwvw             1/1     Running     1 (126m ago)   150m
managed-serviceaccount-addon-agent-6bff74567c-ff9rh   1/1     Running     1 (127m ago)   150m
```

## 2.2 Analyzing the managed cluster

In this exercise you will be using the Red Hat Advanced Cluster Management portal to analyze the managed cluster’s resources. You may use the workshop presentation for examples and guidance.

1. Using Red Hat Advanced Cluster Management, find out what is the cloud provider of the managed cluster.
2. Using Red Hat Advanced Cluster Management, find out the number of nodes that make up the managed cluster. How many CPUs does each node have?
3. Using Red Hat Advanced Cluster Management, check out whether all users can provision new projects on local-cluster (check if the **self-provisioners** ClusterRoleBinding has the system:authenticated:oauth group associated with it).
4. Using Red Hat Advanced Cluster Management, check what **channel version** is associated with local-cluster (stable / candidate / fast) - (Search for **kind:ClusterVersion** CR).

## 2.3 Upgrade the cluster using Advanced Cluster Management

**NOTE**: Do this exercise towards the end of the day. The upgrading process may take up to an hour to complete.

1. Change the **channel version** on the local-cluster from stable-**4.x** to stable-**4.x+1**.
2. Upgrade the cluster using Red Hat Advanced Cluster Management.
