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


# 检索集群的空间标识
{: #containers_spaceid}

可以在 Cloud Foundry 组织和空间上下文内的 {{site.data.keyword.Bluemix_notm}} 帐户中创建集群。
{:shortdesc}

要查找与集群关联的空间标识，请运行以下命令：

```
bx cs cluster-get ClusterName --json
```
{: codeblock}

其中，**ClusterName** 是集群的名称。


例如，运行该命令的输出如下：

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

空间标识是为 **logSpace** 字段指示的值。
空间名称是为 **logSpaceName** 字段指示的值。
组织标识是为 **logOrg** 字段指示的值。
组织名称是为 **logOrgName** 字段指示的值。

如果这些字段为空，那么没有与该集群关联的 CF 组织和空间。



