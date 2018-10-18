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


# Schlüsseleigner für einen Cluster abrufen
{: #containers_key_owner}

Verwenden Sie den Befehl *ibmcloud cs api-key-info*, um den {{site.data.keyword.loganalysisshort}}-Schlüsseleigner für einen Cluster abzurufen.
{:shortdesc}

Führen Sie den folgenden Befehl aus:

```
 ibmcloud cs api-key-info ClusterName
```
{: codeblock}

Dabei ist **ClusterName** der Name des Clusters.


Die Ausgabe kann nach dem Ausführen des Befehls beispielsweise folgendermaßen aussehen:

```
ibmcloud cs api-key-info MyDemoCluster
Getting information about the API key owner for cluster MyDemoCluster...
OK
Name           Email   
Joe Blogg      blogg@ibm.com   
```
{: screen}

Die Bereichs-ID ist der Wert, der für das Feld **logSpace** angegeben ist.
Der Bereichsname ist der Wert, der für das Feld **logSpaceName** angegeben ist.
Die Organisations-ID ist der Wert, der für das Feld **logOrg** angegeben ist.
Der Organisationsname ist der Wert, der für das Feld **logOrgName** angegeben ist.

Wenn diese Felder leer sind, ist diesem Cluster keine CF-Organisation und kein CF-Bereich zugeordnet.



