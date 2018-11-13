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


# Richiamo del proprietario della chiave per un cluster
{: #containers_key_owner}

Utilizza il comando *ibmcloud cs api-key-info* per ottenere il proprietario della chiave {{site.data.keyword.loganalysisshort}} per un cluster.
{:shortdesc}

Esegui il seguente comando:

```
 ibmcloud cs api-key-info ClusterName
```
{: codeblock}

dove **ClusterName** è il nome del cluster.


Ad esempio, l'output di esecuzione del comando è il seguente:

```
ibmcloud cs api-key-info MyDemoCluster
Getting information about the API key owner for cluster MyDemoCluster...
OK
Name           Email   
Joe Blogg      blogg@ibm.com   
```
{: screen}

L'ID spazio è il valore indicato per il campo **logSpace**.
Il nome spazio è il valore indicato per il campo **logSpaceName**.
L'ID organizzazione è il valore indicato per il campo **logOrg**.
Il nome organizzazione è il valore indicato per il campo **logOrgName**.

Se questi campi sono vuoti, non ci sono spazi e organizzazioni CF associati a tale cluster.



