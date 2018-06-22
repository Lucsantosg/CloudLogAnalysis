---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Obtention du jeton IAM
{: #auth_iam}

Pour gérer les journaux qui sont disponibles dans le domaine de compte via l'API {{site.data.keyword.loganalysisshort}}, vous devez utiliser un jeton d'authentification. Utilisez l'interface de ligne de commande {{{site.data.keyword.Bluemix_notm}} pour obtenir le jeton IAM. Le jeton possède un délai d'expiration. 
{:shortdesc}


## Obtention du jeton IAM
{: #iam_token_cli}

Pour obtenir le jeton d'autorisation via l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, procédez comme suit à partir d'un terminal :

1. Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   Pour plus d'informations, voir [Téléchargement et installation de l'interface de ligne de commande {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si l'interface de ligne de commande est installée, passez à l'étape suivante.
    
2. Connectez-vous à une région dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Exécutez la commande `bx iam oauth-tokens` pour obtenir le jeton IAM.

    ```
	bx iam oauth-tokens
	```
	{: codeblock}
	
	La sortie renvoie le jeton IAM que vous devez utiliser pour authentifier votre ID utilisateur dans cet espace et dans cette organisation. Vous pouvez exporter le jeton IAM vers une variable de shell telle que `$iam_token`. 



**Remarque :** lorsque vous utilisez le jeton, retirez *Bearer* de la valeur du jeton que vous avez transmis dans un appel d'API. 

