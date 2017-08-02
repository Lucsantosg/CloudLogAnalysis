---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Mise à disposition du service Log Analysis
{: #provision}

Vous pouvez mettre à disposition le service {{site.data.keyword.loganalysisshort}} à partir de l'interface utilisateur {{site.data.keyword.Bluemix}} ou de la ligne de commande.
{:shortdesc}


## Mise à disposition à partir de l'interface utilisateur
{: #ui}

Pour mettre à disposition une instance du service {{site.data.keyword.loganalysisshort}} dans {{site.data.keyword.Bluemix_notm}} :

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.

    Le tableau de bord {{site.data.keyword.Bluemix_notm}} se trouve à l'adresse suivante : [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.
    
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre. 

2. Cliquez sur **Catalog**. La liste des services disponibles sur {{site.data.keyword.Bluemix_notm}} s'ouvre. 

3. Sélectionnez la catégorie **DevOps** pour filtrer la liste de services affichée. 

4. Cliquez sur la mosaïque **Log Analysis**. 

5. Sélectionnez un plan de service. Par défaut, le plan **Lite** est défini. 

    Pour plus d'informations sur les plans de service, voir [Plans de service](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
6. Cliquez sur **Create** pour mettre à disposition le service {{site.data.keyword.loganalysisshort}} dans l'espace {{site.data.keyword.Bluemix_notm}} auquel vous êtes connecté. 
  
 

## Mise à disposition à partir de l'interface de ligne de commande
{: #cli}

Procédez comme suit pour mettre à disposition une instance du service {{site.data.keyword.loganalysisshort}} dans {{site.data.keyword.Bluemix_notm}} via la ligne de commande : 

1. Installez l'interface de ligne de commande Cloud Foundry (CF). Si l'interface de ligne de commande CF est installée, passez à l'étape suivante.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande cf ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}. 
    
2. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :

    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.
	
3. Exécutez la commande `cf create-service` pour mettre à disposition une instance. 

    ```
	cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}
	
	Où
	
	* service_name est le nom du service, en l'occurrence, **ibmLogAnalysis**.
	* service_plan est le nom du plan de service. Pour obtenir une liste de plans, voir [Plans de service](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	* service_instance_name est le nom que vous souhaitez utiliser pour la nouvelle instance de service que vous créez.
	
	Pour plus d'informations sur la commande cf, voir [cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service).

	Par exemple, pour créer une instance du service {{site.data.keyword.loganalysisshort}} avec un plan gratuit, exécutez la commande suivante :
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}
	
4. Vérifiez que le service a bel et bien été créé. Exécutez la commande suivante :

    ```	
	cf services
	```
	{: codeblock}
	
	Le résultat de l'exécution de la commande se présente comme suit :
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	{: screen}

	



