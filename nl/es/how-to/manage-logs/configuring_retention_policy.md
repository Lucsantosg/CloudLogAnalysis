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

# Configuración de la política de retención de registros
{: #configuring_retention_policy}

Utilice el mandato **cf logging option** para ver y configurar la política de retención que define el número máximo de días que se conservan los registros en el componente de recopilación de registros. De forma predeterminada, los registros se conservan durante 30 días. Una vez transcurrido el periodo de retención, los registros se suprimen automáticamente. De forma predeterminada, la política de retención está inhabilitada.
{:shortdesc}

Puede tener distintas políticas de retención definidas en la cuenta. Puede tener una cuenta de cuenta global y políticas de espacios individuales. La política de retención que se establece a nivel de cuenta establece el número máximo de días que puede conservar los registros. Si establece una política de retención de espacio para un periodo de tiempo superior al periodo de nivel de cuenta, la política que se aplica es la última política que se ha configurado para dicho espacio. 


## Inhabilitación de la política de retención de registros para un espacio
{: #disable_retention_policy_space}

Siga los siguientes pasos para inhabilitar una política de retención:

1. Inicie la sesión en la región, organización o espacio de {{site.data.keyword.Bluemix_notm}} donde desea establecer una política de retención de registros. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Establezca el periodo de retención en **-1** para inhabilitar el periodo de retención. Ejecute el mandato:

    ```
    cf logging option -r -1
    ```
    {: codeblock}
    
**Ejemplo**
    
Por ejemplo, para inhabilitar el periodo de retención para un espacio con el ID *d35da1e3-b345-475f-8502-cfgh436902a3*, ejecute el siguiente mandato:

```
cf logging option -r -1
```
{: codeblock}

La salida es:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen} 



## Comprobación de la política de retención de registros para un espacio
{: #check_retention_policy_space}

Para obtener el periodo de retención establecido para un espacio de {{site.data.keyword.Bluemix_notm}}, siga los pasos siguientes:

1. Inicie la sesión en la región, organización o espacio de {{site.data.keyword.Bluemix_notm}} donde desea establecer una política de retención de registros. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenga el periodo de retención. Ejecute el mandato:

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
    

## Comprobación de la política de retención de registros para todos los espacios de una cuenta
{: #check_retention_policy_account}

Para obtener el periodo de retención establecido para cada espacio de {{site.data.keyword.Bluemix_notm}} de una cuenta, siga los pasos siguientes:

1. Inicie la sesión en la región, organización o espacio de {{site.data.keyword.Bluemix_notm}} donde desea establecer una política de retención de registros. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenga el periodo de retención para cada espacio de la cuenta. Ejecute el mandato:

    ```
    cf logging option -a
    ```
    {: codeblock}

    La salida es:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    | fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Establecimiento de una política de retención de registros a nivel de cuenta
{: #set_retention_policy_space}

Para ver el periodo de retención correspondiente a una cuenta de {{site.data.keyword.Bluemix_notm}}, siga los pasos siguientes:

1. Inicie la sesión en la región, organización o espacio de {{site.data.keyword.Bluemix_notm}} donde desea establecer una política de retención de registros. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Establezca el periodo de retención. Ejecute el mandato:

    ```
    cf logging option -r *Número_de_días* - a
    ```
    {: codeblock}
    
    donde *Número_de_días* es un entero que define el número de días que desea conservar los registros. 
    
    
**Ejemplo**
    
Por ejemplo, para conservar cualquier tipo de registro en su cuenta durante solo 15 días, ejecute el mandato siguiente:

```
cf logging option -r 15 -a
```
{: codeblock}

El resultado muestra una entrada para cada espacio de la cuenta e incluye información sobre el periodo de retención:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        15 |
+--------------------------------------+-----------+
| fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
+--------------------------------------+-----------+
```
{: screen}

## Establecimiento de la política de retención de registros para un espacio
{: #set_retention_policy_account}

Para ver el periodo de retención correspondiente a un espacio de {{site.data.keyword.Bluemix_notm}}, siga los pasos siguientes:

1. Inicie la sesión en la región, organización o espacio de {{site.data.keyword.Bluemix_notm}} donde desea establecer una política de retención de registros. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Establezca el periodo de retención. Ejecute el mandato:

    ```
    cf logging option -r *Número_de_días*
    ```
    {: codeblock}
    
    donde *Número_de_días* es un entero que define el número de días que desea conservar los registros.
    
    
**Ejemplo**
    
Por ejemplo, para conservar los registros disponibles en un espacio durante un año, ejecute el
siguiente
mandato:

```
cf logging option -r 365
```
{: codeblock}

La salida es:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |       365 |
+--------------------------------------+-----------+
```
{: screen}


