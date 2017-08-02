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


# Accès au tableau de bord Kibana
{: #launch}

Vous pouvez lancer Kibana à partir du service {{site.data.keyword.loganalysisshort}}, depuis l'interface utilisateur {{site.data.keyword.Bluemix}} ou directement depuis un
navigateur Web.
{:shortdesc}

Pour les applications CF et les conteneurs Docker qui sont déployés dans une infrastructure cloud gérée par {{site.data.keyword.Bluemix_notm}}, vous pouvez lancer Kibana
depuis {{site.data.keyword.Bluemix_notm}} pour afficher et analyser des données en contexte sur la ressource à partir de laquelle vous lancez Kibana. Par exemple, vous pouvez lancer
dans votre application CF spécifique des journaux dans Kibana, et ce dans le contexte de cette application spécifique.
    
Pour les ressources de cloud comme un conteneur Docker qui sont déployées dans une infrastructure Kubernetes, vous pouvez lancer Kibana depuis un lien de navigateur direct ou depuis le
tableau de bord du service {{site.data.keyword.loganalysisshort}} pour afficher les données de journal ajoutés depuis les services dans un espace
{{site.data.keyword.Bluemix_notm}} fourni. La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté. 

Le tableau suivant recense certaines ressources de cloud et les méthodes de navigation prises en charge pour lancer Kibana :

<table>
<caption>Tableau 1. Liste des ressources et des méthodes de navigation prises en charge. </caption>
  <tr>
    <th>Ressource</th>
	<th>Accès au tableau de bord Kibana depuis le tableau de bord du service {{site.data.keyword.loganalysisshort}}</th>
    <th>Accès au tableau de bord Kibana depuis le tableau de bord Bluemix</th>
    <th>Accès au tableau de bord Kibana depuis un navigateur Web</th>
  </tr>
  <tr>
    <td>Application CF</td>
	<td>Oui</td>
    <td>Oui</td>
    <td>Oui</td>
  </tr>  
  <tr>
    <td>Conteneur déployé dans un cluster Kubernetes</td>
	<td>Oui</td>
    <td>Non</td>
    <td>Oui</td>
  </tr>  
  <tr>
    <td>Conteneur déployé dans une infrastructure de cloud gérée par {{site.data.keyword.Bluemix_notm}}</td>
	<td>Oui</td>
    <td>Oui</td>
    <td>Oui</td>
  </tr>  
</table>

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    

##  Accès à Kibana depuis le tableau de bord du service Log Analysis
{: #launch_Kibana_from_log_analysis}

La requête qui est utilisée pour filtrer les données qui sont affichées dans Kibana extrait les entrées de journal pour cet espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. 
	
Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Effectuez les étapes suivantes pour lancer Kibana depuis le tableau de bord du service {{site.data.keyword.loganalysisshort}} :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} puis cliquez sur le service {{site.data.keyword.loganalysisshort}} depuis le tableau de bord
{{site.data.keyword.Bluemix_notm}}. 
    
2. Sélectionnez l'onglet **Managed** dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.

3. Cliquez sur **LAUNCH**. Le tableau de bord Kibana s'ouvre.

Par défaut, la page **Discover** se charge avec le canevas d'index par défaut sélectionné et un filtre temporel défini sur les 15 dernières minutes. 

Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](filter_logs.html#set_time_filter).

	
	
##  Accès à Kibana depuis un navigateur Web
{: #launch_Kibana_from_browser}

La requête qui est utilisée pour filtrer les données qui sont affichées dans Kibana extrait les entrées de journal pour cet espace dans l'organisation
{{site.data.keyword.Bluemix_notm}}. 
	
Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Pour lancer Kibana depuis un navigateur, procédez comme suit :

1. Ouvrez un navigateur Web et lancez Kibana. Ensuite, connectez-vous à l'interface utilisateur Kibana. 
    
    Par exemple, le tableau suivant indique l'URL que vous devez utiliser pour lancer Kibana dans la région Sud des Etats-Unis :
      
    <table>
          <caption>Tableau 1. URL permettant de lancer Kibana par région</caption>
           <tr>
            <th>Région</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>Sud des États-Unis</td>
            <td>https://logging.ng.bluemix.net/ </td>
          </tr>
    </table>
	
	La page Discover s'ouvre dans Kibana.
	
2. Sélectionnez le canevas d'index pour l'espace {{site.data.keyword.Bluemix_notm}} depuis lequel vous souhaitez afficher et analyser les données de journal.

    1. Cliquez sur **default-index**.
	
	2. Sélectionnez le canevas d'index pour l'espace. Le format du canevas d'index est le suivant :
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    où *Space_ID* est l'identificateur global de l'espace {{site.data.keyword.Bluemix_notm}} où vous souhaitez afficher et analyser les données de journal. 
	
Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


	
##  Accès à Kibana depuis le tableau de bord d'une application CF
{: #launch_Kibana_from_cf_app}

La requête qui est utilisée pour filtrer les données qui s'affichent dans Kibana récupère les entrées de journal pour l'application CF {{site.data.keyword.Bluemix_notm}} depuis
l'endroit où vous lancez Kibana.

Pour visualiser les journaux d'une application Cloud Foundry dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Ouvrez l'onglet des journaux dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}.

    Pour les applications CF, cliquez sur **Journaux** dans la barre de navigation. 
    L'onglet des journaux s'affiche.  

3. Cliquez sur **Advanced view**. Le tableau de bord Kibana s'ouvre.

    Par défaut, la page **Discover** est chargée avec le canevas d'index par défaut et un filtre temporel est défini sur les 30 dernières secondes. La requête de recherche est définie pour porter sur toutes les entrées de votre application CF.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


##  Accès à Kibana depuis le tableau de bord d'un conteneur
{: #launch_Kibana_for_containers}

Cette méthode s'applique uniquement aux conteneurs qui sont déployés dans l'infrastructure de cloud gérée par {{site.data.keyword.Bluemix_notm}}.

La requête qui est utilisée pour filtrer les données qui sont affichées dans Kibana extrait les entrées de journal pour le conteneur depuis lequel vous lancez Kibana.

Pour afficher les journaux d'un conteneur Docker dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le conteneur depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Ouvrez l'onglet des journaux dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}.

    Pour les conteneurs qui sont déployés dans l'infrastructure de cloud gérée par {{site.data.keyword.IBM_notm}}, sélectionnez **Monitoring and logs** dans la
barre de navigation puis cliquez sur l'onglet **Logging**. 
    
    L'onglet des journaux s'affiche.  

3. Cliquez sur **Advanced view**. Le tableau de bord Kibana s'ouvre.

    Par défaut, la page **Discover** est chargée avec le canevas d'index par défaut et un filtre temporel est défini sur les 30 dernières secondes. La
requête de recherche est définie pour porter sur toutes les entrées du conteneur Docker.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).

	



