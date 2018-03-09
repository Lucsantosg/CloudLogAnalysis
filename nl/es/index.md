---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de aprendizaje de iniciación
{: #getting-started-with-cla}

Utilice esta guía de aprendizaje para aprender cómo empezar a trabajar con el servicio {{site.data.keyword.loganalysislong}} en {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Objetivos
{: #objectives}

* Suministrar el servicio {{site.data.keyword.loganalysislong}} en un espacio.
* Configurar la línea de mandatos para gestionar registros.
* Establecer permisos para que un usuario vea registros en un espacio.
* Iniciar Kibana, la herramienta de código abierto que puede utilizar para ver registros.


## Antes de empezar
{: #prereqs}

Debe tener un ID de usuario que sea miembro o un propietario de una cuenta de {{site.data.keyword.Bluemix_notm}}. Para obtener un ID de usuario de {{site.data.keyword.Bluemix_notm}}, vaya a: [Registro ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/registration/){:new_window}

Esta guía de aprendizaje proporciona instrucciones para suministrar y trabajar con el servicio {{site.data.keyword.loganalysisshort}} en la región EE.UU. sur.


## Paso 1: Suministrar el servicio {{site.data.keyword.loganalysisshort}}
{: #step1}

**Nota:** Suministre una instancia del servicio {{site.data.keyword.loganalysisshort}} en un espacio de Cloud Foundry (CF). Solo necesita una instancia del servicio por espacio. No puede suministrar el servicio {{site.data.keyword.loganalysisshort}} a nivel de cuenta. 

Siga estos pasos para suministrar una instancia del servicio {{site.data.keyword.loganalysisshort}} en {{site.data.keyword.Bluemix_notm}}:

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}.  

2. Seleccione la región, la organización y el espacio donde desea suministrar el servicio {{site.data.keyword.loganalysisshort}}.  

3. Pulse **Catálogo**. Se abrirá la lista de servicios disponibles en {{site.data.keyword.Bluemix_notm}}.

4. Seleccione la categoría **DevOps** para filtrar la lista de servicios mostrados.

5. Pulse el mosaico **Análisis de registros**.

6. Seleccione un plan de servicio. De forma predeterminada, se establece el plan **Lite**.

    Para obtener más información sobre los planes de servicio, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
7. Pulse **Crear** para suministrar el servicio {{site.data.keyword.loganalysisshort}} en el espacio de {{site.data.keyword.Bluemix_notm}} en el que ha iniciado sesión.




## Paso 2: [Opcional] Cambiar el plan de servicio para el servicio {{site.data.keyword.loganalysisshort}}
{: #step2}

Si necesita más cuota de búsqueda, almacenamiento a largo plazo de registros, o ambos, puede cambiar el plan de instancia de servicio {{site.data.keyword.loganalysisshort}} mediante la IU de {{site.data.keyword.Bluemix_notm}} o ejecutando el mandato `bx cf update-service` para habilitar estas características. 

Puede actualizar o reducir el plan de servicio en cualquier momento.

Para obtener más información, consulte [Planes de servicio {{site.data.keyword.loganalysisshort}}](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

**NOTA:** Cambiar el plan a un plan de pago tiene un coste.

Para cambiar el plan de servicio en la IU de {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}.  

2. Seleccione la región, la organización y el espacio donde está disponible el servicio de {{site.data.keyword.loganalysisshort}}.  

3. Pulse la instancia de servicio de {{site.data.keyword.loganalysisshort}} desde el *Panel de control* de {{site.data.keyword.Bluemix_notm}}. 
    
4. Seleccione el separador **Plan** en el panel de control de {{site.data.keyword.loganalysisshort}}.

    Se muestra información sobre el plan actual.
	
5. Seleccione un plan nuevo para actualizar o reducir su plan. 

6. Pulse **Guardar**.



## Paso 3: Configurar el entorno local para trabajar con el servicio {{site.data.keyword.loganalysisshort}}
{: #step3}


El servicio {{site.data.keyword.loganalysisshort}} incluye una interfaz de línea de mandatos (CLI) que puede utilizar para gestionar registros que se almacenan en la Recopilación de registros (componente de almacenamiento a largo plazo). 

Puede utilizar el plugin de {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} para ver el estado del registro, para descargar registros y para configurar la política de retención de registros.  

La CLI ofrece distintos tipos de ayuda: ayuda general para obtener información sobre la CLI y los mandatos soportados, ayuda sobre mandatos para ver cómo se utiliza un mandato o ayuda sobre submandatos para aprender a utilizar un submandato de un mandato.


Para instalar la CLI de {{site.data.keyword.loganalysisshort}} desde el repositorio de {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Instale el plugin de {{site.data.keyword.loganalysisshort}}.Ejecute el mandato siguiente:

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. Compruebe que el plugin de {{site.data.keyword.loganalysisshort}} esté instalado.
  
    Por ejemplo, ejecute el siguiente mandato para ver la lista de plugins instalados:
    
    ```
    bx plugin list
 ```
    {: codeblock}
    
    La salida tiene el aspecto siguiente:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version
    logging-cli          0.1.1
 ```
    {: screen}




## Paso 4: Establecer permisos para que un usuario vea registros
{: #step4}

Para controlar las acciones de {{site.data.keyword.loganalysisshort}} que puede realizar un usuario, puede asignar roles y políticas a un usuario. 

Hay dos tipos de permisos de seguridad en {{site.data.keyword.Bluemix_notm}} que controlan las acciones que pueden realizar los usuarios cuando trabajan con el servicio {{site.data.keyword.loganalysisshort}}:

* Roles de Cloud Foundry (CF): Otorgue un rol de CF a un usuario para definir los permisos que tiene el usuario para ver registros en un espacio.
* Roles de IAM: Otorgue una política de IAM a un usuario para definir los permisos que tiene el usuario para ver registros en el dominio de la cuenta, y los permisos que tiene el usuario para gestionar registros almacenados en la Recopilación de registros. 


Siga estos pasos para otorgar permisos a un usuario para ver registros en un espacio:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Cuando inicia sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

4. Seleccione **Acceso de Cloud Foundry** y, a continuación, seleccione la organización.

    Se listará la lista de espacios disponibles en dicha organización.

5. Seleccione el espacio donde se suministra el servicio de {{site.data.keyword.loganalysisshort}}. A continuación, desde la acción de menú, seleccione **Editar el rol de espacio**.

6. Seleccione *Auditor*. 

    Puede seleccionar uno o más roles de espacio. Todos los roles siguientes permiten a un usuario ver registros: *Gestor*, *Desarrollador*, y *Auditor*
	
7. Pulse **Guardar rol**.


Para obtener más información, consulte [Concesión de permisos](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).



## Paso 5: Iniciar Kibana
{: #step5}

Para ver y analizar los datos de registro, debe acceder a Kibana en la región Pública de la nube donde están disponibles los datos de registro. 


Para iniciar Kibana en la región EE.UU. sur, abra un navegador web y escriba el siguiente URL:

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


Para obtener más información sobre cómo iniciar Kibana en otras regiones, consulte [Navegación a Kibana desde un navegador web](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

**Nota:** Cuando inicie Kibana, si obtiene un mensaje que indica *señal de transporte no válida*, compruebe sus permisos en el espacio. Este mensaje es una indicación de que el ID de usuario no tiene permisos para ver registros.
    

## Pasos siguientes 
{: #next_steps}

Generar registros. Pruebe con cualquiera de las siguientes guías de aprendizaje:

* [Análisis de registros en Kibana para una app desplegada en un clúster de Kubernetes](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    Esta guía de aprendizaje muestra los pasos necesarios para hacer que funcione el siguiente caso de ejemplo completo: Suministrar un clúster, configurar el clúster para enviar registros al servicio de {{site.data.keyword.loganalysisshort}} en {{site.data.keyword.Bluemix_notm}}, desplegar una app en el clúster, y utilizar Kibana para ver y filtrar registros de contenedor para dicho clúster.     
    
* [Análisis de registros en Kibana para una app de Cloud Foundry](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    Esta guía de aprendizaje muestra los pasos necesarios para hacer que funcione el siguiente caso de ejemplo completo: Desplegar una aplicación de Python Cloud Foundry, generar distintos tipos de registros y utilizar Kibana para ver, buscar y analizar registros de CF.
   








