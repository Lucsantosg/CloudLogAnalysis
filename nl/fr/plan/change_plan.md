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


# Modification du plan
{: #change_plan}

Votre pouvez changer de plan de service {{site.data.keyword.loganalysisshort}} dans {{site.data.keyword.Bluemix_notm}} dans le tableau de bord du service ou en exécutant la commande `cf update-service`. Vous
pouvez mettre à niveau ou réduire votre plan à tout moment.
{:shortdesc}

## Modification du plan de service via l'interface utilisateur
{: #change_plan_ui}

Pour changer de plan de service dans {{site.data.keyword.Bluemix_notm}} depuis le tableau de bord du service, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} puis cliquez sur le service {{site.data.keyword.loganalysisshort}} depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Sélectionnez l'onglet **Plan** dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.

    Des informations sur votre plan en cours s'affichent.
	
3. Sélectionnez un nouveau plan pour mettre à jour ou réduire votre plan. 

4. Cliquez sur **Sauvegarder**.



## Modification du plan de service via l'interface de ligne de commande
{: #change_plan_cli}

Pour modifier votre plan de service dans Bluemix via l'interface de ligne de commande, procédez comme suit :

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
	
2. Exécutez la commande `cf services` pour vérifier votre plan en cours et pour obtenir le nom de service {{site.data.keyword.loganalysisshort}} dans la liste
des services disponibles dans l'espace. 

    La valeur de la zone **name** est celle que vous devez utiliser pour modifier le plan. 

    Par exemple
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Mettez à niveau ou réduisez votre plan. Exécutez la commande `cf update-service`.
    
	```
	cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	où 
	
	* *service_name* est le nom de votre service. Vous pouvez exécuter la commande `cf services` pour obtenir la valeur.
	* *new_plan* est le nom du plan.
	
	Le tableau suivant présente les différents plans et les valeurs prises en charge :
	
	<table>
	  <caption>Tableau 1. Liste des plans.</caption>
	  <tr>
	    <th>Plan</th>
	    <th>Nom</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>Collecte de journaux</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>Collecte de journaux avec recherche de 2 Go/jour</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>Collecte de journaux avec recherche de 5 Go/jour</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>Collecte de journaux avec recherche de 10 Go/jour</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	Par exemple, pour réduire votre plan au plan *Lite*, exécutez la commande suivante :
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Vérifiez que le nouveau plan est modifié. Exécutez la commande `cf services`.

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






