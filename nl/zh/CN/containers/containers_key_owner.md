---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 检索集群的密钥所有者
{: #containers_key_owner}

使用 *ibmcloud cs api-key-info* 命令以获取集群的 {{site.data.keyword.loganalysisshort}} 密钥所有者。
{:shortdesc}

运行以下命令：

```
 ibmcloud cs api-key-info ClusterName
```
{: codeblock}

其中，**ClusterName** 是集群的名称。


例如，运行该命令的输出如下：

```
ibmcloud cs api-key-info MyDemoCluster
Getting information about the API key owner for cluster MyDemoCluster...
OK
Name           Email   
Joe Blogg      blogg@ibm.com   
```
{: screen}

空间标识是为 **logSpace** 字段指示的值。
空间名称是为 **logSpaceName** 字段指示的值。
组织标识是为 **logOrg** 字段指示的值。
组织名称是为 **logOrgName** 字段指示的值。

如果这些字段为空，说明没有与该集群关联的 CF 组织和空间。



