---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Retrieving the space ID for a cluster
{: #containers_spaceid}

You can create a cluster in an {{site.data.keyword.Bluemix_notm}} account within the context of a Cloud Foundry organization and space. 
{:shortdesc}

To find the space ID that is associated with a cluster, run the following command:

```
bx cs cluster-get ClusterName --json
```
{: codeblock}

where **ClusterName** is the name of the cluster.


For example, the output of running the command is the following:

```
{
    "id": "c213f81296db4c68b84e212c19135a99",
    "name": "MyDemoCluster",
    "region": "us-south",
    "dataCenter": "hou02",
    "location": "us-south-hou02",
    "serverURL": "https://xxx.xx.xx.xx:xxxxx",
    "state": "normal",
    "createdDate": "2017-09-26T09:00:59+0000",
    "modifiedDate": "2017-11-29T05:30:41+0000",
    "workerCount": 5,
    "isPaid": true,
    "masterKubeVersion": "1.7.4_1504",
    "targetVersion": "1.7.4_1504",
    "ingressHostname": "",
    "ingressSecretName": "",
    "logOrg": "5eab56t3-dty7-4utc-adaa-3aa5gn7r4g41",
    "logOrgName": "MyOrg",
    "logSpace": "fa277ff8-8a73-324b-9b75-0f11d54a3ae2",
    "logSpaceName": "MySpace",
    "addons": null,
    "vlans": null
}
```
{: screen}

The space ID is the value indicated for the **logSpace** field.
The space name is the value indicated for the **logSpaceName** field.
The organization ID is the value indicated for the **logOrg** field.
The organization name is the value indicated for the **logOrgName** field.

If these fields are empty, then, there is no CF organization and space associated to that cluster.



