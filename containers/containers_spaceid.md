---

copyright:
  years: 2017

lastupdated: "2017-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Retrieving the space ID for a cluster
{: #containers_spaceid}

When a cluster is created in an {{site.data.keyword.Bluemix_notm}} account, the logs are associated with a space within that account. When you create queries to view cluster logs, you need the space ID.
{:shortdesc}

To find the space ID for a cluster, run the folloing command:

```
bx cs cluster-get cluster-name
```
{: codeblock}

where **cluster-name** is the name of the cluster.

The space ID is the value indicated for the **Log Space** field.

For example, the output of running the command is the following:

```
Name:			    cluster-name
ID:			        c213f81296db4c68b84e212c19135a99
State:			    normal
Created:		    2017-08-22T18:18:59+0000
Datacenter:		    dal10
Master URL:		    https://169.46.7.242:21210
Ingress subdomain:  cluster-name.us-south.containers.mybluemix.net
Ingress secret:     cluster-name
Workers:		    5
Log Space:		    fa277ff8-8a73-324b-9b75-0f11d54a3ae2
```
{: screen}