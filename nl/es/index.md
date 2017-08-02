---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de aprendizaje de iniciación
{: #getting-started-with-cla}

En esta guía de iniciación, revisaremos los pasos a seguir para realizar tareas avanzadas de análisis mediante el servicio {{site.data.keyword.loganalysislong}}. Aprenda a buscar y analizar los registros de contenedor de una app desplegada en un clúster Kubernetes.
{:shortdesc}

## Antes de empezar
{: #prereqs}

Cree una [cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/). El ID de usuario debe ser un miembro o un propietario de una cuenta {{site.data.keyword.Bluemix_notm}} con permisos para crear clústeres Kubernetes, desplegar apps en clústeres y realizar consultas en los registros de {{site.data.keyword.Bluemix_notm}} para un análisis avanzado en Kibana.

Abra una sesión de terminal desde la que gestionar el clúster Kubernetes y desplegar apps desde la línea de mandatos. Los ejemplos en esta guía de aprendizaje se proporcionan para un sistema Ubuntu Linux.

[Instale los plug-ins de interfaz de línea de mandatos](/docs/containers/cs_cli_install.html#cs_cli_install_steps) en su entorno local para gestionar {{site.data.keyword.containershort}} desde la línea de mandatos. 



## Paso 1: Desplegar una app en un clúster Kubernetes
{: #step1}

1. [Crear un clúster Kubernetes](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. [Configurar el contexto del clúster](/docs/containers/cs_cli_install.html#cs_cli_configure) en un terminal Linux. Después de haber configurado el contexto, podrá gestionar el clúster Kubernetes y desplegar la aplicación en dicho clúster Kubernetes.

3. Desplegar y ejecutar una app de ejemplo en el clúster Kubernetes. [Complete los pasos de la lección 1](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

    La app es una app Node.js Hello World:

    ```
    var express = require('express')
    var app = express()

    app.get('/', function(req, res) {
      res.send('Hello world! Your app is up and running in a cluster!\n')
    })
    app.listen(8080, function() {
      console.log('Sample app is listening on port 8080.')
    })
    ```
	{: codeblock}

    Cuando se despliega la app, la recopilación del registro se habilita de forma automática para todas las entradas de registro que envíe la app a stdout (salida estándar) y stderr (error estándar). 

    En esta app de ejemplo, cuando prueba la app en un navegador, la app escribe en la salida estándar el siguiente mensaje: `Sample app is listening on port 8080.`

## Paso 2: Navegar al panel de control de Kibana
{: #step2}

Para analizar los datos de registro para un clúster, debe acceder a Kibana en la región Pública de la nube en la que se ha creado el clúster. 

Por ejemplo, para iniciar Kibana en la región EE. UU. sur, navegue al URL siguiente:

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}

    
    
## Paso 3: Analizar datos de registro en Kibana
{: #step3}

1. En la página **Descubrir**, mire los sucesos que se visualizan. 

    La aplicación Hello-World genera un suceso.
    
    En la sección Campos disponibles, puede ver una lista de campos para utilizar para definir nuevas consultas o para filtrar las entradas que aparecen listadas en la tabla que se visualiza en la página.
    
    En la siguiente tabla se muestra una lista de campos comunes que puede utilizar para definir nuevas consultas de búsquedas. En la tabla también se incluyen valores de ejemplo que corresponden al suceso que la app de ejemplo genera:
    
     <table>
              <caption>Tabla 2. Campos comunes para registros de contenedor </caption>
               <tr>
                <th align="center">Campo</th>
                <th align="center">Descripción</th>
                <th align="center">Ejemplo</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> El valor de este campo corresponde al GUID del contenedor que ejecuta la app en un pod del clúster Kubernetes.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>El valor de este campo corresponde a la región de {{site.data.keyword.Bluemix_notm}} en la que se recopila esta entrada de registro.</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>El valor de este campo informa sobre el nombre del contenedor.</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>El valor de este campo informe sobre la IP pública que está disponible para acceder a la app desde internet. </td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>Los campos de etiqueta son opcionales. Puede haber 0 o más etiquetas. Cada etiqueta empieza con el prefijo `kubernetes.labels.` seguido por *nombre_etiqueta*. </td>
                <td>En la app de ejemplo, puede ver dos etiquetas: <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>El valor de este campo informa sobre el espacio de nombres de Kubernetes donde está el pod en ejecución. </td>
                <td>default</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>El valor de este campo corresponde al GUID del pod donde se ejecuta el contenedor. </td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>El valor de este campo informa sobre el nombre de pod.</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>Se trata el mensaje completo que registra la aplicación.</td>
                <td>Sample app is listening on port 8080.</td>
              </tr>
        </table>
    
2. Filtrar datos en la página **Descubrir**.  

    En la tabla podrá ver todas las entradas disponibles para ser analizadas. Las entradas que se listan corresponden a la consulta de búsqueda que se visualiza en la barra Buscar. El asterisco (*) es el carácter que se utiliza para visualizar todas las entradas del periodo de tiempo configurado para la página. 
    
    Por ejemplo, para filtrar datos según el espacio de nombres de Kubernetes, modifique la barra de consulta Buscar. Añada un filtro en base al campo personalizado *kubernetes.namespace_name_str*:
    
    1. En la sección *Campos disponibles*, seleccione el campo *kubernetes.namespace_name_str*. Se visualizará un subconjunto de valores disponibles para el campo.    
    
    2. Seleccione el valor **default**. Este es el espacio de nombres donde en el paso anterior se desplegó la app de ejemplo.
    
        Después de seleccionar el valor, se añade un filtro a la barra Buscar para que la tabla visualice únicamente las entradas que coincidan con el criterio que acaba de seleccionar.     
    
    Puede seleccionar el símbolo de edición del filtro para modificar el nombre del espacio de nombres que busca.   
    
    Se visualiza la siguiente consulta:
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "default",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Para buscar entradas en un espacio de nombres diferente como, por ejemplo, *mynamespace1*, modifique la consulta:
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "mynamespace1",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Si no ve ningún dato, intente cambiar el filtro de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Para obtener más información, consulte [Filtrado de registros en Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).


## Pasos siguientes
{: #next_steps}

A continuación, cree los paneles de control de Kibana. Para obtener más información, consulte [Análisis de registros en Kibana mediante un panel de control](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
                                                                                                                      

