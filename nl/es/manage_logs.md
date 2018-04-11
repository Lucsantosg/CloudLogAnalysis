---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Gestión de registros
{: #manage_logs}

Puede utilizar la CLI de {{site.data.keyword.loganalysisshort}} y la API de {{site.data.keyword.loganalysisshort}} para gestionar los registros que se almacenan en la recopilación de registros.{:shortdesc}

Para gestionar registros, tenga en cuenta la siguiente información:

1. El ID de usuario debe tener una política asignada en {{site.data.keyword.Bluemix_notm}} para {{site.data.keyword.loganalysisshort}} con permisos para gestionar registros.  

    Para ver una lista de los roles de IAM y de las tareas por rol, consulte [Roles de IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles). 
	
	Para obtener más información sobre cómo asignar una política, consulte [Asignación de una política de IAM a un usuario mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).
	
2. Esta característica solo está disponible para los planes de servicio que permiten la retención de registros.  

    Para obtener más información sobre los planes de servicio, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

El servicio {{site.data.keyword.loganalysisshort}} ofrece dos CLI que puede utilizar para gestionar registros:

* Un plugin de {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la CLI, consulte [CLI de {{site.data.keyword.loganalysisshort}} (plugin de {{site.data.keyword.Bluemix_notm}})](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#log_analysis_cli).
* Un plugin de {{site.data.keyword.loganalysisshort}} CF (en desuso). Para obtener más información sobre la CLI, consulte [Configuración de la CLI de análisis de registros (plugin de CF)](/docs/services/CloudLogAnalysis/reference/logging_cli.html#logging_cli).


## Configuración de una política de retención de registros
{: #log_retention_policy}

Puede utilizar la CLI de {{site.data.keyword.loganalysisshort}} para ver y configurar una política de retención de registros. La política especifica el número de días que los registros se conservan en el componente de recopilación de registros. 

* De forma predeterminada, cuando selecciona un plan de pago, los registros se recopilan y se conservan en la recopilación de registros. 
* Si define un periodo de retención, una vez transcurrido el periodo de retención, los registros se suprimen automáticamente del componente de recopilación de registros y no se pueden recuperar.
* Puede especificar un periodo de retención para una cuenta. El periodo de retención se configura automáticamente para todos los espacios de esa cuenta. 
* Puede especificar un periodo de retención para un espacio.
* Puede cambiar la política de retención siempre que lo desee.
* Para inhabilitar la política, establezca su valor en *-1*. 

**Nota:** Cuando se inhabilita la política de retención de registros, se deben mantener los registros en el componente de recopilación de registros. Puede utilizar el mandato de la CLI [cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#delete) para suprimir los registros antiguos.

Para obtener más información, consulte:

* [Visualización y configuración de la política de retención de registros mediante el plugin de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy_cloud.html#configuring_retention_policy).
* [Visualización y configuración de la política de retención de registro mediante el plugin de CF](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy.html#configuring_retention_policy).


## Supresión de registros
{: #log_deletion}

Los registros que se almacenan en búsqueda de registros se suprimen transcurridos 3 días.

Registros que se almacenan en el componente de recopilación de registro se conservan hasta que el usuario configura una política de retención o hasta que los suprime manualmente. 

* Puede configurar una política de retención de registros para definir el número de días que desea conservar los registros en la recopilación de registros. Para obtener más información, consulte:

    [Visualización y configuración de la política de retención de registros mediante el plugin de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy_cloud.html#configuring_retention_policy).
	
	[Visualización y configuración de la política de retención de registro mediante el plugin de CF](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy.html#configuring_retention_policy).

    Para inhabilitar la política, establezca su valor en *-1*. 

* Puede utilizar la [API de recopilación de registros](https://console.bluemix.net/apidocs/948-ibm-cloud-log-collection-api?&language=node&env_id=ibm%3Ayp%3Aus-south#introduction){: new_window} o la [CLI de recopilación de registros](/docs/services/CloudLogAnalysis/reference/logging_cli.html#logging_cli){: new_window} para suprimir registros manualmente del componente de recopilación de registros.  

* Puede utilizar la CLI. Para obtener más información sobre cómo suprimir registros manualmente mediante la CLI, consulte:

    [bx logging log-delete mediante el plugin de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/how-to/manage-logs/deleting_logs_cloud.html#deleting_logs).
    
	[bx cf logging delete mediante el plugin de CF](/docs/services/CloudLogAnalysis/reference/logging_cli.html#delete).


## Descarga de registros
{: #download_logs}

Puede buscar los registros correspondientes a los 3 últimos días en Kibana. Para poder analizar datos de registro más antiguos, puede descargar los registros en un archivo local, o bien puede dirigir estos registros a otros programas como, por ejemplo, Elastic Stack local. 

Para obtener más información, consulte:

* [Descarga de registros mediante el plugin de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/how-to/manage-logs/downloading_logs_cloud.html#downloading_logs).
* [Descarga de registros mediante el plugin de CF](/docs/services/CloudLogAnalysis/how-to/manage-logs/downloading_logs.html#downloading_logs).




## Obtención de información sobre sus registros
{: #info_about_logs}

Para obtener información general sobre sus registros, utilice el mandato `bx logging log-show` o el mandato `cf logging status`. Para obtener más información, consulte:

* [Visualización de información de registro mediante el plugin de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information_cloud.html#viewing_log_status)
* [Visualización de información de registro mediante el plugin de CF](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information.html#viewing_log_status).

Por ejemplo, para mantener el coste bajo control, es posible que desee supervisar el tamaño de los registros de sus apps durante un periodo de tiempo. Por ejemplo, quizás desee saber el tamaño de cada tipo de registro durante una semana para un espacio de {{site.data.keyword.Bluemix_notm}} a fin de identificar si alguna app o servicio está generando más registros de los esperados. Para comprobar el tamaño de sus registros, utilice el mandato `bx logging log-show` o el mandato `cf logging status`. 

Puede ver información sobre los registros almacenados en un dominio del espacio, en un dominio de la organización o en un dominio de la cuenta.



## Instalación de la CLI de {{site.data.keyword.loganalysisshort_notm}} (plugin de CF)
{: #install_cli}

Para ver cómo se instala la CLI, consulte [Instalación de la CLI de registro](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#config_log_collection_cli).

Para comprobar la versión de la CLI, ejecute el mandato [bx cf logging](/docs/services/CloudLogAnalysis/reference/logging_cli.html#base) con el parámetro * -version*.

Para obtener ayuda sobre cómo se ejecutan los mandatos, consulte [Obtención de ayuda en línea de mandatos para ejecutar mandatos](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#command_cli_help).

## Instalación de la CLI de {{site.data.keyword.loganalysisshort_notm}} (plugin de {{site.data.keyword.Bluemix_notm}}) 
{: #install_cli}

Para ver cómo se instala la CLI, consulte [Instalación de la CLI de registro](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#config_log_collection_cli).

Para comprobar la versión de la CLI, ejecute el mandato `bx plugin list`. 

Para obtener ayuda sobre cómo se ejecutan los mandatos, consulte [Obtención de ayuda en línea de mandatos para ejecutar mandatos](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#command_cli_help).


## Puntos finales de registro
{: #endpoints}

En la tabla siguiente se muestran los URL de registro por región:

<table>
    <caption>Puntos finales por región</caption>
    <tr>
      <th>Región</th>
      <th>URL</th>
    </tr>
	<tr>
      <td>Frankfurt</td>
	  <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
    </tr>
	<tr>
      <td>Sídney</td>
	  <td>[https://logging.au-syd.bluemix.net](https://logging.au-syd.bluemix.net)</td>
    </tr>
	<tr>
      <td>Reino Unido</td>
	  <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
    </tr>
    <tr>
      <td>EE.UU. sur</td>
      <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
    </tr>
</table>

## Roles que necesita un usuario para gestionar registros
{: #roles}

En {{site.data.keyword.Bluemix_notm}}, puede asignar uno o varios roles a los usuarios. Estos roles definen qué tareas están habilitadas para dicho usuario para trabajar con el servicio de {{site.data.keyword.loganalysisshort}}. 

Las tablas siguientes muestran los roles que debe tener un usuario para gestionar registros:

<table>
  <caption>Permisos que necesita un **propietario de cuenta** para gestionar registros</caption>
  <tr>
	<th>Rol de IAM</th>
	<th>Acciones</th>
  </tr>
  <tr>
    <td>*Administrador*</td>
    <td>Comprobar el estado de los registros </br>Descargar registros </br>Suprimir registros </br>Cambiar la política de retención de registros </br>Gestionar sesiones</td>
</table>

<table>
  <caption>Permisos que necesita un **auditor** para gestionar registros</caption>
  <tr>
	<th>Rol de IAM</th>
	<th>Acciones</th>
  </tr>
  <tr>
    <td>*Visor*</td>
    <td>Obtener información sobre los registros contenidos en el componente de recopilación de registros. </br>Obtener información sobre la política de retención de registros que se ha configurado. </td>
</table>

<table>
  <caption>Permisos que necesita un **administrador** para gestionar registros</caption>
  <tr>
	<th>Rol de IAM</th>
	<th>Acciones</th>
  </tr>
  <tr>
    <td>*Administrador*</td>
    <td>Comprobar el estado de los registros </br>Descargar registros </br>Suprimir registros </br>Cambiar la política de retención de registros </br>Gestionar sesiones</td>
</table>

<table>
  <caption>Permisos que necesita un **desarrollador** para gestionar registros.</caption>
  <tr>
	<th>Rol de IAM</th>
	<th>Acciones</th>
  </tr>
  <tr>
    <td>*Editor
*</td>
    <td>Comprobar el estado de los registros </br>Descargar registros </br>Suprimir registros </br>Cambiar la política de retención de registros </br>Gestionar sesiones</td>
</table>
