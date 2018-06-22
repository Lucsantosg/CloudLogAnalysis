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


# Obtention du jeton UAA
{: #auth_uaa}

Pour gérer les journaux à l'aide de l'API {{site.data.keyword.loganalysisshort}}, vous devez utiliser un jeton d'authentification. Utilisez l'interface de ligne de commande {{site.data.keyword.loganalysisshort}} pour obtenir le jeton UAA. Le jeton possède un délai d'expiration. 
{:shortdesc}

		
## Obtention du jeton UAA via l'interface de ligne de commande Log Analysis (plug-in CF)
{: #uaa_cli}


Pour obtenir le jeton d'autorisation, procédez comme suit :

1. Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   Pour plus d'informations, voir [Téléchargement et installation de l'interface de ligne de commande {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si l'interface de ligne de commande est installée, passez à l'étape suivante.
    
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Exécutez la commande `bx cf oauth-token` pour obtenir le jeton UAA {{site.data.keyword.Bluemix_notm}}.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	La sortie renvoie le jeton UAA que vous devez utiliser pour authentifier votre ID utilisateur dans cet espace et dans cette organisation.
	

**Remarque :** lorsque vous utilisez le jeton, retirez *Bearer* de la valeur du jeton que vous avez transmis dans un appel d'API. 
