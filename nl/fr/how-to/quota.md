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


# Calcul du quota de recherche et de l'utilisation quotidienne
{: #quota}

Pour obtenir le quota et l'utilisation quotidienne actuelle d'un domaine de journaux du service {{site.data.keyword.loganalysisshort}}, vous pouvez exécuter une commande cURL. 
{:shortdesc}


## Calcul du quota de recherche et de l'utilisation quotidienne d'un compte
{: #account}

Procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Obtenez l'ID du compte. Exécutez la commande suivante :

    ```
	bx iam accounts
	```
    {: codeblock}	

	La liste des comptes et de leur identificateur global unique s'affiche.
	
	Exportez l'ID de compte dans une variable de shell. Exemple :
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. Obtenez le jeton UAA. 

    Pour plus d'informations, voir [Obtention du jeton UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exportez le jeton UAA dans une variable de shell. N'incluez pas le préfixe `Bearer`. Exemple :
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenez le quota du domaine et l'utilisation actuelle. Exécutez la commande suivante :

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	où *ENDPOINT* est différent selon la région. Pour la liste des noeuds finaux par région, voir [Noeuds finaux de journalisation](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	Par exemple, exécutez la commande cURL afin d'obtenir le quota pour le compte dans la région Sud des Etats-Unis :
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	Le résultat inclut les informations relatives à l'utilisation et au quota quotidiens.
	
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

	
## Calcul du quota de recherche et de l'utilisation quotidienne d'un espace
{: #space}

Procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Obtenez l'ID de l'espace.

    Pour plus d'informations, voir [Comment obtenir l'identificateur global unique d'un espace ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).
	
	Exportez l'ID d'espace dans une variable de shell. Exemple :
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. Obtenez le jeton UAA. 

    Pour plus d'informations, voir [Obtention du jeton UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exportez le jeton UAA dans une variable de shell. N'incluez pas le préfixe `Bearer`. Exemple :
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Obtenez le quota du domaine et l'utilisation actuelle. Exécutez la commande suivante :

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	où *ENDPOINT* est différent selon la région. Pour la liste des noeuds finaux par région, voir [Noeuds finaux de journalisation](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

    Par exemple, exécutez la commande cURL suivante pour obtenir le quota et l'utilisation d'un domaine d'espace dans la région Sud des Etats-Unis :
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	Le résultat inclut les informations relatives à l'utilisation et au quota quotidiens.
	
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



