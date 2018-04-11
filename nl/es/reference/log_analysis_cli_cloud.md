---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# CLI de Log Analysis (plugin de {{site.data.keyword.Bluemix_notm}})
{: #log_analysis_cli}

La CLI de {{site.data.keyword.loganalysislong}} es un plug-in de {{site.data.keyword.Bluemix_notm}} que puede utilizar para gestionar los registros almacenados en el componente de recopilación de registros.
{: shortdesc}

**Requisitos previos**
* Antes de ejecutar mandatos de registro, inicie una sesión en {{site.data.keyword.Bluemix_notm}} con el mandato `bx login` para generar una señal de acceso y autenticar la sesión.

Para obtener información sobre la utilización de la interfaz de línea de mandatos de {{site.data.keyword.loganalysisshort}}, consulte [Gestión de registros](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov).

<table>
  <caption>Mandatos para gestionar registros</caption>
  <tr>
    <th>Mandato</th>
    <th>Cuándo utilizarlo</th>
  </tr>
  <tr>
    <td>[bx logging](#base)</td>
    <td>Utilice este mandato para obtener información sobre la CLI, como por ejemplo la lista de mandatos.</td>
  </tr>
  <tr>
    <td>[bx logging log-delete](#delete)</td>
    <td>Utilice este mandato para suprimir los registros almacenados en el componente de recopilación de registros.</td>
  </tr>
  <tr>
    <td>[bx logging log-download](#download)</td>
    <td>Utilice este mandato para descargar de la recopilación de registros en un archivo local, o para direccionar los registros a otro programa, como por ejemplo Elastic Stack. </td>
  </tr>
  <tr>
    <td>[bx logging help](#help)</td>
    <td>Utilice este mandato para obtener ayuda sobre cómo utilizar la CLI y una lista de todos los mandatos.</td>
  </tr>
  <tr>
    <td>[bx logging option-show](#optionshow)</td>
    <td>Utilice este mandato para ver el periodo de retención para los registros que están disponibles en un espacio, una organización o una cuenta.</td>
  </tr>
  <tr>
    <td>[bx logging option-update](#optionupdate)</td>
    <td>Utilice este mandato para establecer el periodo de retención para los registros que están disponibles en un espacio, una organización o una cuenta.</td>
  </tr>
  <tr>
    <td>[bx logging session-create
](#session_create)</td>
    <td>Utilice este mandato para crear una nueva sesión.</td>
  <tr>
  <tr>
    <td>[bx logging session-delete](#session_delete)</td>
    <td>Utilice este mandato para suprimir una sesión.</td>
  <tr>  
  <tr>
    <td>[bx logging sessions](#session_list)</td>
    <td>Utilice este mandato para obtener una lista de las sesiones activas y sus ID.</td>
  <tr>  
  <tr>
    <td>[bx logging session-show](#session_show)</td>
    <td>Utilice este mandato para ver el estado de una sesión individual.</td>
  <tr>  
  <tr>
    <td>[bx logging log-show](#status)</td>
    <td>Utilice este mandato para obtener información sobre los registros que se han recopilado en un espacio, organización o cuenta.</td>
  </tr>
</table>


## bx logging
{: #base}

Proporciona información general sobre la CLI.

```
bx logging 
```
{: codeblock}

**Ejemplos**

Para obtener la lista de mandatos, ejecute el mandato siguiente:

```
bx logging
NAME:
   bx logging - IBM Cloud Log Analysis Service
USAGE:
   bx logging command [argumentos...] [opciones de mandato]

MANDATOS:
   log-delete       Suprimir registro
   log-download     Descargar un registro
   log-show         Mostrar el recuento, tamaño y tipo de registros por día
   session-create   Crear una sesión
   session-delete   Suprimir sesión
   sessions         Mostrar información sobre las sesiones
   session-show     Mostrar información de una sesión
   option-show      Mostrar la retención de registros
   option-update    Mostrar las opciones de registro
   help             
   
Indique 'bx logging help [mandato]' para obtener más información sobre un mandato.
```
{: codeblock}




## bx logging log-delete
{: #delete}

Suprime los registros almacenados en el componente de recopilación de registros.

```
bx logging log-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-f, --force ]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>-f, --force </dt>
  <dd>(Opcional) Establezca esta opción para suprimir los registros sin tener que confirmar la acción.
  </dd>
</dl>

**Ejemplo**

Para suprimir los registros de tipo *linux_syslog* del 25 de mayo de 2017, ejecute el mandato siguiente:
```
bx logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: screen}



## bx logging log-download 
{: #download}

Descarga los registros del componente de recopilación de registros en un archivo local o direcciona los registros a otro programa, como por ejemplo Elastic Stack. 

**Nota:** Para descargar archivos, primero tiene que crear una sesión. Una sesión define los registros que se van a descargar en función de rango de fechas, tipo de registro y tipo de cuenta. Los registros se descargan dentro del contexto de una sesión. Para obtener más información, consulte [bx logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create).

```
 bx logging log-download  [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-o, --output OUTPUT] SESSION_ID

```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
 
  <dt>-o, --output OUTPUT</dt>
  <dd>(Opcional) Establece la vía de acceso y el nombre del archivo de salida local en el que se descargan los registros. <br>El valor predeterminado es un guión (-). <br>Establezca este parámetro en el valor predeterminado para dirigir los registros a la salida estándar.</dd>

</dl>

**Argumentos**

<dl>
  <dt>SESSION_ID</dt>
  <dd>Este valor indica el ID de la sesión que debe utilizar al descargar los registros. <br>**Nota:** El mandato `bx logging session-create` proporciona los parámetros que controlan los registros que se descargan. </dd>
</dl>

**Nota:** Una vez finalizada la descarga, si se intenta ejecutar el mismo mandato de nuevo, este no hará nada. Para volver a descargar los mismos datos, debe utilizar otro archivo u otra sesión.

**Ejemplos**

En un sistema Linux, para descargar registros en un archivo denominado mylogs.gz, ejecute el mandato siguiente:

```
bx logging log-download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

Para descargar registros en su propia plataforma Elastic Stack, ejecute el mandato siguiente:

```
bx logging log-download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
```
{: screen}

A continuación verá un ejemplo de archivo logstash.conf:

```
input {
  stdin {
    codec => json_lines {}
  }
}
output {
  elasticsearch {
    hosts => [ "127.0.0.1:9200" ]
  }
}
```
{: screen}


## bx logging help
{: #help}

Proporciona información sobre cómo utilizar un mandato.

```
bx logging help [mandato] 
```
{: codeblock}

**Parámetros**

<dl>
<dt>Mandato</dt>
<dd>Establezca el nombre del mandato para el que desea obtener ayuda.
</dd>
</dl>


**Ejemplos**

Para obtener ayuda sobre cómo ejecutar el mandato para ver el estado de los registros, ejecute el mandato siguiente:

```
bx logging help log-show
NOMBRE:
   log-show - Mostrar el recuento, tamaño y tipo de los registros por día

USO:
   bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]

OPCIONES:
   -r, --resource-type     Tipo de recurso, los tipos de recurso válidos son account, org o space
   -i, --resource-id       ID de recurso, el ID del recurso de destino
   -s, --start             Fecha de inicio, valor en hora UTC especificado en formato AAAA-MM-DD
   -e, --end               Fecha final, valor en hora UTC especificado en formato AAAA-MM-DD
   -t, --type              Tipo de registro, por ejemplo "syslog"
   -l, --list-type-detail  Mostrar el tipo detallado

```
{: screen}


## bx logging option-show
{: #optionshow}

Muestra el periodo de retención para los registros que están disponibles en un espacio, una organización o una cuenta. 

* El periodo se establece en número de días.
* El valor predeterminado es **-1**. 

**Nota:** de forma predeterminada, se almacenan todos los registros. Debe suprimirlos manualmente mediante el mandato **delete**. Defina una política de retención para suprimir registros automáticamente.

```
bx logging option-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>

</dl>

**Ejemplos**

Para ver el periodo de retención actual predeterminado para el espacio en el que ha iniciado la sesión, ejecute el mandato siguiente:

```
bx logging option-show
```
{: screen}




## bx logging option-update
{: #optionupdate}

Cambia el periodo de retención para los registros que están disponibles en un espacio, una organización o una cuenta. 

* El periodo se establece en número de días.
* El valor predeterminado es **-1**. 

```
bx logging option-update [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] <-e,--retention RETENTION_VALUE>
```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
  
  <dt>-e,--retention RETENTION_VALUE</dt>
  <dd>Establece el número de días que los registros se conservan. </dd>

</dl>

**Ejemplo**

Para cambiar el periodo de retención por 25 días para el espacio en el que ha iniciado la sesión, ejecute el mandato siguiente:

```
bx logging option-update -e 25
```
{: screen}



## bx logging session-create
{: #session_create}

Crea una nueva sesión.

**Nota:** Puede tener un máximo de 30 sesiones simultáneas en un espacio. La sesión se crea para un usuario. Las sesiones no se pueden compartir entre usuarios de un espacio.

```
bx logging session-create [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Opcional) Define el tipo de registro. <br>Por ejemplo, *syslog* es un tipo de registro. <br>El valor predeterminado es asterisco (*). <br>Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo *log_type_1,log_type_2,log_type_3*.
  </dd>

</dl>


**Valores que se devuelven**

<dl>

    <dt>ID</dt>
    <dd>ID de sesión.</dd>
	
	<dt>Tipo de recurso</dt>
    <dd>ID de recurso.</dd>

    <dt>AccessTime</dt>
    <dd>Indicación de fecha y hora que muestra cuándo se ha utilizado la sesión por última vez.</dd>

    <dt>CreateTime</dt>
    <dd>Indicación de fecha y hora correspondiente a la fecha y hora en que se ha creado la sesión.</dd>
	
	<dt>Start</dt>
    <dd>Indica el primer día que se utiliza para filtrar registros. </dd>

    <dt>End</dt>
    <dd>Indica el último día que se utiliza para filtrar registros.</dd>

    <dt>Type</dt>
    <dd>Los tipos de registro que se descargan a través de la sesión.</dd>

</dl>


**Ejemplo**

Para crear una sesión que incluya registros correspondientes al 13 de noviembre de 2017, ejecute el siguiente mandato:

```
bx logging session-create -s 2017-11-13 -e 2017-11-13
Creating session for xxxxx@yyy.com resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   2017-11-13   2017-11-13   ANY_TYPE
Session: 1ef776d1-4d25-4297-9693-882606c725c8 is created
```
{: screen}


## bx logging session-delete 
{: #session_delete}

Suprime una sesión, especificada por ID de sesión.

```
bx session-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID
```
{: codeblock}

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
 
</dl>

**Argumentos**

<dl>
  <dt>SESSION_ID</dt>
  <dd>ID de la sesión activa que desea suprimir.</dd>
</dl>

**Ejemplo**

Para suprimir una sesión con el ID de sesión *cI6hvAa0KR_tyhjxZZz9Uw==*, ejecute el mandato siguiente:

```
bx logging session-delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## bx logging sessions
{: #session_list}

Muestra una lista de las sesiones activas y sus ID.

```
bx logging sessions [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parámetros**

<dl>

  <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión.  </dd>
</dl>

**Valores de retorno**

<dl>	
    <dt>SESSION_ID</dt>
    <dd>ID de la sesión activa.</dd>
	   
    <dt>ID de recurso</dt>
    <dd>ID del recurso para el que es válida la sesión.</dd>

    <dt>CreateTime</dt>
    <dd>Indicación de fecha y hora correspondiente a la fecha y hora en que se ha creado la sesión.</dd>

    <dt>AccessTime</dt>
    <dd>Indicación de fecha y hora que muestra cuándo se ha utilizado la sesión por última vez.</dd>
</dl>
 
**Ejemplo**

```
bx logging sessions
Listing sessions of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z
Listed the sessions of resource xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
:{ screen}


## bx logging session-show
{: #session_show}

Muestra el estado de una sesión individual.

```
bx logging session-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID

```
{: codeblock}

**Parámetros**

<dl>
   <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión.  </dd>
</dl>

**Argumentos**

<dl>
   <dt>SESSION_ID</dt>
   <dd>ID de la sesión activa sobre la que desea obtener información.</dd>
</dl>

**Ejemplo**

Para mostrar los detalles de una sesión con el ID de sesión *cI6hvAa0KR_tyhjxZZz9Uw==*, ejecute el mandato siguiente:

```
bx logging session-show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}


## bx logging log-show
{: #status}

Devuelve información sobre los registros que se han recopilado en un espacio o cuenta de {{site.data.keyword.Bluemix_notm}}.

```
bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]
```
{: codeblock}

* Si no se especifica el tipo de recurso, el mandato devuelve los detalles del recurso en el que ha iniciado la sesión.
* Si especifica un tipo de recurso, debe especificar el ID de recurso.
* El mandato solo muestra información sobre las 2 últimas semanas de registros que se han almacenado en el componente de recopilación de registros cuando no se especifican fechas inicial y final.

**Parámetros**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Establece el tipo de recurso. Los valores válidos son *space*, *account* y *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Establezca este campo en el ID del espacio, la organización o la cuenta sobre la que desea obtener información. <br>De forma predeterminada, si no especifica este parámetro, el mandato utiliza el ID del recurso en el que ha iniciado la sesión. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Opcional) Define el tipo de registro. <br>Por ejemplo, *syslog* es un tipo de registro. <br>El valor predeterminado es asterisco (*). <br>Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>-l, --list-type-detail</dt>
  <dd>(Opcional) Defina este parámetro para obtener una lista de cada tipo de registro individualmente.
  </dd>
</dl>


**Ejemplo**

```
bx logging log-show
Showing log status of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

Date         Size        Count    Searchable   Types
2017-11-07   1878197     1333     None         default
2017-11-13   201653512   179391   All          default,linux_syslog
2017-11-14   32134119    30425    All          default,linux_syslog
2017-11-15   303901156   269689   All          linux_syslog,default
2017-11-16   107253679   96648    All          default,linux_syslog   
```
{: screen}

```
 bx logging log-show -l
Showing log status of resource: cedc73c5-6d55-4193-a9de-378620d6fab5 ...

Date         Size        Count    Searchable   Type
2017-11-14   30146764    26611    true         default
2017-11-14   1987355     3814     true         linux_syslog
2017-11-15   303004895   267890   true         default
2017-11-15   896261      1799     true         linux_syslog
2017-11-16   107918249   96278    true         default
2017-11-16   912890      1794     true         linux_syslog   
```
{: screen}