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


# Extraction du propriétaire de clé pour un cluster
{: #containers_key_owner}

Utilisez la commande *ibmcloud cs api-key-info* afin d'obtenir le propriétaire de clé {{site.data.keyword.loganalysisshort}} pour un cluster.
{:shortdesc}

Exécutez la commande suivante :

```
 ibmcloud cs api-key-info ClusterName
```
{: codeblock}

où **ClusterName** est le nom du cluster.


Par exemple, la sortie de l'exécution de la commande est la suivante :

```
ibmcloud cs api-key-info MyDemoCluster
Getting information about the API key owner for cluster MyDemoCluster...
OK
Name           Email   
Joe Blogg      blogg@ibm.com   
```
{: screen}

L'ID d'espace est la valeur indiquée dans la zone **logSpace**.
Le nom d'espace est la valeur indiquée dans la zone **logSpaceName**.
L'ID d'organisation est la valeur indiquée dans la zone **logOrg**.
Le nom d'organisation est la valeur indiquée dans la zone **logOrgName**.

Si ces zones sont vides, cela signifie qu'aucun espace ni organisation CF n'est associé à ce cluster.



