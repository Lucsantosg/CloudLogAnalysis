---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Cálculo de la cuota de búsqueda y del uso diario
{: #quota}

Para obtener la cuota y el uso diario actual de un dominio de registros del servicio {{site.data.keyword.loganalysisshort}}, puede ejecutar un mandato cURL. {:shortdesc}


## Cálculo de la cuota de búsqueda y del uso diario de una cuenta
{: #account}

Siga estos pasos:

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Obtenga el ID de la cuenta. Ejecute el mandato siguiente:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Una lista de cuentas en las que se visualiza los GUID.
	
	Exporte el ID de la cuenta a una variable de shell. Por ejemplo:
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. Obtenga la señal de UAA.

    Para obtener más información, consulte [Obtención de la señal de UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exporte la señal de UAA a una variable de shell. No incluya `Bearer`. Por ejemplo:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenga la cuota del dominio y el uso actual. Ejecute el mandato siguiente:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	donde *ENDPOINT* varía según la región. Para ver una lista de los puntos finales por región, consulte [Puntos finales de registro](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	Por ejemplo, ejecute este mandato cURL para obtener la cuota correspondiente a la cuenta de la región EE.UU. Sur:
```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	El resultado incluye información sobre la cuota y el uso diario.

	 	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

  

   {
      "usage": {
 "dailyallotment": 524288000,
        "current": 2115811531
       }
 }
    ```
    {: screen}

	
## Cálculo de la cuota de uso y del uso diario de un espacio
{: #space}

Siga estos pasos:

1. Inicie la sesión en {{site.data.keyword.Bluemix_notm}}.

  Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

 2. Obtenga el ID del espacio.
Para obtener más información, consulte [Cómo se obtiene el GUID de un espacio](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  	
Exporte el ID del espacio a una variable de shell. Por ejemplo:
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. Obtenga la señal de UAA.

    Para obtener más información, consulte [Obtención de la señal de UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exporte la señal de UAA a una variable de shell. No incluya `Bearer`. Por ejemplo:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenga la cuota del dominio y el uso actual. Ejecute el mandato siguiente:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	donde *ENDPOINT* varía según la región. Para ver una lista de los puntos finales por región, consulte [Puntos finales de registro](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	Por ejemplo, ejecute el siguiente mandato cURL para obtener la cuota y el uso de un dominio de espacio de la región EE.UU. Sur:

```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	El resultado incluye información sobre la cuota y el uso diario.

	 	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

  

   {
      "usage": {
 "dailyallotment": 524288000,
        "current": 2115811531
       }
 }
    ```
    {: screen}


