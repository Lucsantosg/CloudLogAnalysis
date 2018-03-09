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


# Recuperación del propietario de la clave de un clúster
{: #containers_key_owner}

Utilice el mandato *bx cs api-key-info* para obtener el propietario de la clave de {{site.data.keyword.loganalysisshort}} de un clúster.
{:shortdesc}

Ejecute el mandato siguiente:

```
 bx cs api-key-info ClusterName
```
{: codeblock}

donde **ClusterName** es el nombre del clúster.


Por ejemplo, el resultado de ejecutar el mandato es el siguiente: 

```
bx cs api-key-info MyDemoCluster
Getting information about the API key owner for cluster MyDemoCluster...
OK
Name           Email   
Joe Blogg      blogg@ibm.com   
```
{: screen}

El ID de espacio es el valor indicado para el campo **logSpace**.
El nombre de espacio es el valor indicado para el campo **logSpaceName**.
El ID de organización es el valor indicado para el campo **logOrg**.
El nombre de la organización es el valor indicado para el campo **logOrgName**.

Si estos campos están vacíos, no habrá ninguna organización ni espacio de CF asociados con dicho clúster.



