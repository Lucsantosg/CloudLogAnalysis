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

# CLI de IBM Cloud Log Analysis
{: #logging_cli}

La CLI de {{site.data.keyword.loganalysislong}} es un plugin para gestionar los registros correspondientes a los recursos de nube que se ejecutan en un espacio de una organización de {{site.data.keyword.Bluemix}}.
{: shortdesc}

**Requisitos previos**
* Antes de ejecutar mandatos de registro, inicie una sesión en {{site.data.keyword.Bluemix_notm}} con el mandato `cf login` para generar una señal de acceso de {{site.data.keyword.Bluemix_short}} y autenticar la sesión.

Para obtener información sobre la utilización de la interfaz de línea de mandatos de {{site.data.keyword.loganalysisshort}}, consulte [Gestión de registros](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov).

<table>
  <caption>Mandatos para gestionar registros</caption>
  <tr>
    <th>Mandato</th>
    <th>Cuándo utilizarlo</th>
  </tr>
  <tr>
    <td>[cf logging](#base)</td>
    <td>Utilice este mandato para obtener información sobre la CLI, como por ejemplo la versión o la lista de mandatos.</td>
  </tr>
  <tr>
    <td>[cf logging auth](#auth)</td>
    <td>Utilice este mandato para obtener la señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}.</td>
  </tr>
  <tr>
    <td>[cf logging delete](#delete)</td>
    <td>Utilice este mandato para suprimir los registros almacenados en el componente de recopilación de registros.</td>
  </tr>
  <tr>
    <td>[cf logging download (Beta)](#download)</td>
    <td>Utilice este mandato para descargar de la recopilación de registros en un archivo local, o para direccionar los registros a otro programa, como por ejemplo una pila ELK. </td>
  </tr>
  <tr>
    <td>[cf logging help](#help)</td>
    <td>Utilice este mandato para obtener ayuda sobre cómo utilizar la CLI y una lista de todos los mandatos.</td>
  </tr>
  <tr>
    <td>[cf logging option](#option)</td>
    <td>Utilice este mandato para ver o definir el periodo de retención para los registros que están disponibles en un espacio o una cuenta de {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  <tr>
    <td>[cf logging session create (Beta)](#session_create)</td>
    <td>Utilice este mandato para crear una nueva sesión.</td>
  <tr>
  <tr>
    <td>[cf logging session delete (Beta)](#session_delete)</td>
    <td>Utilice este mandato para suprimir una sesión.</td>
  <tr>  
  <tr>
    <td>[cf logging session list (Beta)](#session_list)</td>
    <td>Utilice este mandato para obtener una lista de las sesiones activas y sus ID.</td>
  <tr>  
  <tr>
    <td>[cf logging session show (Beta)](#session_show)</td>
    <td>Utilice este mandato para ver el estado de una sesión individual.</td>
  <tr>  
  <tr>
    <td>[cf logging status](#status)</td>
    <td>Utilice este mandato para obtener información sobre los registros que se han recopilado en un espacio o cuenta de {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  </table>


## cf logging
{: #base}

Proporciona información sobre la versión de la CLI y sobre cómo utilizar la CLI.

```
cf logging [parámetros]
```
{: codeblock}

**Parámetros**

<dl>
<dt>--help, -h</dt>
<dd>Establezca este parámetro para mostrar la lista de mandatos o para obtener ayuda para un mandato.
</dd>

<dt>--version, -v</dt>
<dd>Establezca este parámetro para que se muestre la versión de la CLI.</dd>
</dl>

**Ejemplos**

Para obtener la lista de mandatos, ejecute el mandato siguiente:

```
cf logging --help
```
{: codeblock}

Para obtener la versión de la CLI, ejecute el mandato siguiente:

```
cf logging --version
```
{: codeblock}


## cf logging auth
{: #auth}

Devuelve una señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}. 

**Nota:** La señal no caduca.

```
cf logging auth
```
{: codeblock}

**Devuelve**

<dl>
  <dt>Señal de registro</dt>
  <dd>Por ejemplo, `jec8BmipiEZc`.
  </dd>
  
  <dt>ID de organización</dt>
  <dd>GUID de la organización de {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión.
  </dd>
  
  <dt>ID de espacio</dt>
  <dd>GUID del espacio de la organización en el que ha iniciado la sesión.
  </dd>
</dl>

## cf logging delete
{: #delete}

Suprime los registros almacenados en el componente de recopilación de registros.

```
cf logging delete [parámetros]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>--start valor, -s valor</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>--end valor, -e valor</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD* <br>El formato UTC de la fecha es **AAAA-MM-DD**, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>--type valor, -t valor</dt>
  <dd>(Opcional) Define el tipo de registro. <br>Por ejemplo, *syslog* es un tipo de registro. <br>El valor predeterminado es **\***. <br>Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo **log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Opcional) Establece el ámbito de la información de registro que se proporciona a nivel de cuenta. <br>Si no se especifica este parámetro, el valor predeterminado se establece de modo que se proporciona información de registro solo sobre el espacio actual.
  </dd>
</dl>

**Ejemplo**

Para suprimir los registros de tipo *linux_syslog* del 25 de mayo de 2017, ejecute el mandato siguiente:
```
cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: codeblock}



## cf logging download (Beta)
{: #download}

Descarga los registros del componente de recopilación de registros en un archivo local o direcciona los registros a otro programa, como por ejemplo Elastic Stack. 

**Nota:** Para descargar archivos, primero tiene que crear una sesión. Una sesión define los registros que se van a descargar en función de rango de fechas, tipo de registro y tipo de cuenta. Los registros se descargan dentro del contexto de una sesión. Para obtener más información, consulte [cf logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_create).

```
cf logging download [parámetros] [argumentos]
```
{: codeblock}

**Parámetros**

<dl>
<dt>--output valor, -o valor</dt>
<dd>(Opcional) Establece la vía de acceso y el nombre del archivo de salida local en el que se descargan los registros. <br>El valor predeterminado es un guión (-). <br>Establezca este parámetro en el valor predeterminado para dirigir los registros a la salida estándar.</dd>
</dl>

**Argumentos**

<dl>
<dt>ID_sesión</dt>
<dd>Establezca el valor de ID de sesión que se obtiene cuando se ejecuta el mandato `cf logging session create`. Este valor indica la sesión que se utilizará para descargar los registros. <br>**Nota:** El mandato `cf logging session create` proporciona los parámetros que controlan los registros que se descargan. </dd>
</dl>

**Nota:** Una vez finalizada la descarga, si se intenta ejecutar el mismo mandato de nuevo, este no hará nada. Para volver a descargar los mismos datos, debe utilizar otro archivo u otra sesión.

**Ejemplos**

Para descargar registros en un archivo denominado mylogs.gz, ejecute el mandato siguiente:

```
cf logging download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

Para descargar registros en su propia plataforma Elastic Stack, ejecute el mandato siguiente:

```
cf logging download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
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


## cf logging help
{: #help}

Proporciona información sobre cómo utilizar un mandato.

```
cf logging help [parámetros]
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
cf logging help status
```
{: codeblock}


## cf logging option
{: #option}

Muestra o cambia el periodo de retención para los registros que están disponibles en un espacio o una cuenta de {{site.data.keyword.Bluemix_notm}}. 

* El periodo se establece en número de días.
* El valor predeterminado es **-1**. 

**Nota:** de forma predeterminada, se almacenan todos los registros. Debe suprimirlos manualmente mediante el mandato **delete**. Defina una política de retención para suprimir registros automáticamente.

```
cf logging option [parámetros]
```
{: codeblock}

**Parámetros**

<dl>
<dt>--retention valor, -r valor</dt>
<dd>(Opcional) Define el número de días de retención. <br> El valor predeterminado es 30 días.</dd>

<dt>--at-account-level, -a </dt>
  <dd>(Opcional) Establece el ámbito a nivel de cuenta. <br>**Nota:** Defina este valor para obtener información sobre la cuenta. <br>Si no se especifica este parámetro, el valor predeterminado se establece en *-1* para el espacio actual, que es el espacio donde ha iniciado la sesión mediante el mandato `cf login`.
  </dd>
</dl>

**Ejemplos**

Para ver el periodo de retención actual para el espacio en el que ha iniciado la sesión, ejecute el mandato siguiente:

```
cf logging option
```
{: codeblock}

La salida es:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
+--------------------------------------+-----------+
```
{: screen}


Para cambiar el periodo de retención por 25 días para el espacio en el que ha iniciado la sesión, ejecute el mandato siguiente:

```
cf logging option -r 25
```
{: codeblock}

La salida es:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        25 |
+--------------------------------------+-----------+
```
{: screen}


## cf logging session create (Beta)
{: #session_create}

Crea una nueva sesión.

**Nota:** Puede tener un máximo de 30 sesiones simultáneas en un espacio. La sesión se crea para un usuario. Las sesiones no se pueden compartir entre usuarios de un espacio.

```
cf logging session create [parámetros]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>--start valor, -s valor</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>--end valor, -e valor</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>--type valor, -t valor</dt>
  <dd>(Opcional) Define el tipo de registro. <br>Por ejemplo, *syslog* es un tipo de registro. <br>El valor predeterminado es asterisco (*). <br>Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Opcional) Establece el ámbito a nivel de cuenta. <br>**Nota:** Defina este valor para obtener información sobre la cuenta. <br>Si no se especifica este parámetro, el valor predeterminado se establece en solo el espacio actual, es decir, el espacio donde ha iniciado la sesión mediante el mandato `cf login`.
  </dd>
</dl>

**Valores que se devuelven**

<dl>
<dt>Access-Time</dt>
<dd>Indicación de fecha y hora que muestra cuándo se ha utilizado la sesión por última vez.</dd>

<dt>Create-Time</dt>
<dd>Indicación de fecha y hora correspondiente a la fecha y hora en que se ha creado la sesión.</dd>

<dt>Date-Range</dt>
<dd>Indica los días que se utilizan para filtrar registros. Los registros identificados en este rango de fechas están disponibles para la gestión mediante la sesión.</dd>

<dt>ID</dt>
<dd>ID de sesión.</dd>

<dt>Space</dt>
<dd>ID del espacio en el que la sesión está activa.</dd>

<dt>Type-Account</dt>
<dd>Los tipos de registro que se descargan a través de la sesión.</dd>

<dt>Username</dt>
<dd>ID de {{site.data.keyword.IBM_notm}} del usuario que ha creado la sesión.</dd>
</dl>


**Ejemplo**

Para crear una sesión que incluya los registros comprendidos entre el 20 de mayo de 2017 y el 26 de mayo de 2017 para el tipo de registro *log*, ejecute el mandato siguiente:

```
cf logging session create -s 2017-05-20 -e 2017-05-26 -t log
```
{: screen}


## cf logging session delete (Beta)
{: #session_delete}

Suprime una sesión, especificada por ID de sesión.

```
cf logging session delete [argumentos]
```
{: codeblock}

**Argumentos**

<dl>
<dt>ID de
sesión</dt>
<dd>ID de la sesión que desea suprimir. <br>Puede utilizar el mandato `cf logging session list` para obtener todos los ID de sesiones activas.</dd>
</dl>

**Ejemplo**

Para suprimir una sesión con el ID de sesión *cI6hvAa0KR_tyhjxZZz9Uw==*, ejecute el mandato siguiente:

```
cf logging session delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## cf logging session list (Beta)
{: #session_list}

Muestra una lista de las sesiones activas y sus ID.

```
cf logging session list 
```
{: codeblock}

**Valores que se devuelven**

<dl>
<dt>ID</dt>
<dd>ID de sesión.</dd>

<dt>SPACE</dt>
<dd>ID del espacio en el que la sesión está activa.</dd>

<dt>USERNAME</dt>
<dd>ID de {{site.data.keyword.IBM_notm}} del usuario que ha creado la sesión.</dd>

<dt>CREATE-TIME</dt>
<dd>Indicación de fecha y hora correspondiente a la fecha y hora en que se ha creado la sesión.</dd>

<dt>ACCESS-TIME</dt>
<dd>Indicación de fecha y hora que muestra cuándo se ha utilizado la sesión por última vez.</dd>
</dl>
 

## cf logging session show (Beta)
{: #session_show}

Muestra el estado de una sesión individual.

```
cf logging session show [argumentos]
```
{: codeblock}

**Argumentos**

<dl>
<dt>ID_sesión</dt>
<dd>ID de la sesión activa sobre la que desea obtener información.</dd>
</dl>

**Valores que se devuelven**

<dl>
<dt>Access-Time</dt>
<dd></dd>

<dt>Create-Time</dt>
<dd>Indicación de fecha y hora correspondiente a la fecha y hora en que se ha creado la sesión.</dd>

<dt>Date-Range</dt>
<dd>Indica los días que se utilizan para filtrar registros. Los registros identificados en este rango de fechas están disponibles para la gestión mediante la sesión.</dd>

<dt>ID</dt>
<dd>ID de sesión.</dd>

<dt>Space</dt>
<dd>ID del espacio en el que la sesión está activa.</dd>

<dt>Type-Account</dt>
<dd>Los tipos de registro que se descargan a través de la sesión.</dd>

<dt>Username</dt>
<dd>ID de {{site.data.keyword.IBM_notm}} del usuario que ha creado la sesión.</dd>
</dl>

**Ejemplo**

Para mostrar los detalles de una sesión con el ID de sesión *cI6hvAa0KR_tyhjxZZz9Uw==*, ejecute el mandato siguiente:

```
cf logging session show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}


## cf logging status
{: #status}

Devuelve información sobre los registros que se han recopilado en un espacio o cuenta de {{site.data.keyword.Bluemix_notm}}.

```
cf logging status [parámetros]
```
{: codeblock}

**Parámetros**

<dl>
  <dt>--start valor, -s valor</dt>
  <dd>(Opcional) Establece la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es hace 2 semanas.
  </dd>
  
  <dt>--end valor, -e valor</dt>
  <dd>(Opcional) Establece la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*, por ejemplo `2006-01-02`. <br>El valor predeterminado es la fecha actual.
  </dd>
  
  <dt>--type valor, -t valor</dt>
  <dd>(Opcional) Define el tipo de registro. <br>Por ejemplo, *syslog* es un tipo de registro. <br>El valor predeterminado es asterisco (*). <br>Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Opcional) Establece el ámbito a nivel de cuenta. <br> **Nota:** Defina este valor para obtener información sobre la cuenta. <br>Si no se especifica este parámetro, el valor predeterminado se establece en solo el espacio actual, es decir, el espacio donde ha iniciado la sesión mediante el mandato `cf login`.
  </dd>
  
  <dt>--list-type-detail, -l</dt>
  <dd>(Opcional) Defina este parámetro para obtener una lista del subtotal de tipos de registro para cada día.
  </dd>
</dl>

**Nota:** El mandato `cf logging status` solo muestra las 2 últimas semanas de registros que se han almacenado en el componente de recopilación de registros cuando no se especifican fechas inicial y final.


