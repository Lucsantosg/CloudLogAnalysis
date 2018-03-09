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


# Calculando a cota de procura e o uso diário
{: #quota}

Para obter a cota e uso diário atual de um domínio de logs do serviço {{site.data.keyword.loganalysisshort}}, é possível executar um comando cURL. 
{:shortdesc}


## Calculando a cota de procura e o uso diário de uma conta
{: #account}

Conclua as etapas a seguir:

1. Efetue login na {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Obtenha o ID da conta. Execute o comando a seguir:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Uma lista de contas com seus GUIDs é exibida.
	
	Exporte o ID da conta para uma variável shell. Por exemplo:
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. Obtenha o token do UAA. 

    Para obter mais informações, veja [Obtendo o token do UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exporte o token do UAA para uma variável shell. Não inclua `Bearer`. Por exemplo:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenha a cota do domínio e o uso atual. Execute o comando a seguir:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	em que *ENDPOINT* é diferente por região. Para obter uma lista de terminais por região, veja [Terminais de criação de log](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	Por exemplo, execute o comando cURL para obter a cota para a conta na região Sul dos EUA:
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	O resultado inclui as informações sobre a cota e o uso diários.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "uso": {
        "dailyallotment": 524288000, "current": 2115811531 }
    }
    ```
    {: screen}

	
## Calculando a cota de procura e o uso diário de um espaço
{: #space}

Conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Obtenha o ID do espaço.

    Para obter mais informações, veja [Como obter o GUID de um espaço](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).
	
	Exporte o ID do espaço para uma variável shell. Por exemplo:
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. Obtenha o token do UAA. 

    Para obter mais informações, veja [Obtendo o token do UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exporte o token do UAA para uma variável shell. Não inclua `Bearer`. Por exemplo:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenha a cota do domínio e o uso atual. Execute o comando a seguir:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	em que *ENDPOINT* é diferente por região. Para obter uma lista de terminais por região, veja [Terminais de criação de log](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

    Por exemplo, execute o comando cURL a seguir para obter a cota e uso de um domínio de espaço na região Sul dos EUA:
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	O resultado inclui as informações sobre a cota e o uso diários.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "uso": {
        "dailyallotment": 524288000, "current": 2115811531 }
    }
    ```
    {: screen}



