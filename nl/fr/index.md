---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutoriel d'initiation
{: #getting-started-with-cla}

Suivez ce tutoriel pour commencer à utiliser le service {{site.data.keyword.loganalysislong}} dans {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Objectifs
{: #objectives}

* Mettre à disposition le service {{site.data.keyword.loganalysislong}} dans un espace. 
* Configurer la ligne de commande pour gérer les journaux. 
* Définir les droits d'un utilisateur de sorte qu'il puisse afficher les journaux dans un espace. 
* Lancer Kibana, l'outil open source que vous pouvez utiliser pour afficher les journaux. 


## Avant de commencer
{: #prereqs}

Vous devez disposer d'un ID utilisateur membre ou propriétaire d'un compte {{site.data.keyword.Bluemix_notm}}. Pour obtenir un ID utilisateur {{site.data.keyword.Bluemix_notm}}, accédez à : [Page d'inscription ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/registration/){:new_window}

Ce tutoriel fournit des instructions de mise à disposition et d'utilisation du service {{site.data.keyword.loganalysisshort}} dans la région Sud des Etats-Unis. 


## Etape 1 : Mise à disposition du service {{site.data.keyword.loganalysisshort}} 
{: #step1}

**Remarque :** vous mettez à disposition une instance du service {{site.data.keyword.loganalysisshort}} dans un espace Cloud Foundry (CF). Une seule instance du service par espace est nécessaire. Vous ne pouvez pas mettre à disposition le service {{site.data.keyword.loganalysisshort}} au niveau du compte.  

Procédez comme suit pour mettre à disposition une instance du service {{site.data.keyword.loganalysisshort}} dans {{site.data.keyword.Bluemix_notm}} :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}.  

2. Sélectionnez la région, l'organisation et l'espace où mettre à disposition le service {{site.data.keyword.loganalysisshort}}.   

3. Cliquez sur **Catalogue**. La liste des services disponibles dans {{site.data.keyword.Bluemix_notm}} s'affiche.

4. Sélectionnez la catégorie **DevOps** pour filtrer la liste de services affichée.

5. Cliquez sur la vignette **Log Analysis**.

6. Sélectionnez un plan de service. Par défaut, le plan **Lite** est défini.

    Pour plus d'informations sur les plans de service, voir [Plans de service](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
7. Cliquez sur **Créer** pour mettre à disposition le service {{site.data.keyword.loganalysisshort}} dans l'espace {{site.data.keyword.Bluemix_notm}} auquel vous êtes connecté.




## Etape 2 : [Facultatif] Changement du plan de service pour le service {{site.data.keyword.loganalysisshort}} 
{: #step2}

Si vous avez besoin d'un quota de recherche plus élevé et/ou d'un stockage à long terme des journaux, vous pouvez changer le plan de votre instance de service {{site.data.keyword.loganalysisshort}} depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou en exécutant la commande `bx cf update-service` pour activer ces fonctions.  

Vous pouvez passer à un plan de niveau inférieur ou supérieur à tout moment. 

Pour plus d'informations, voir [Plans de service {{site.data.keyword.loganalysisshort}}](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

**REMARQUE :** le passage à un plan payant a un coût. 

Pour changer le plan de service depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, procédez comme suit : 

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}.  

2. Sélectionnez la région, l'organisation et l'espace où le service {{site.data.keyword.loganalysisshort}} est disponible.   

3. Cliquez sur l'instance de service {{site.data.keyword.loganalysisshort}} dans le *tableau de bord* {{site.data.keyword.Bluemix_notm}}.  
    
4. Sélectionnez l'onglet **Plan** dans le tableau de bord {{site.data.keyword.loganalysisshort}}.

    Des informations sur le plan en cours s'affichent.
	
5. Sélectionnez un nouveau plan de niveau supérieur ou inférieur. 

6. Cliquez sur **Sauvegarder**.



## Etape 3 : Configuration de votre environnement local en vue de l'utilisation du service {{site.data.keyword.loganalysisshort}} 
{: #step3}


Le service {{site.data.keyword.loganalysisshort}} inclut une interface de ligne de commande que vous pouvez utiliser pour gérer les journaux qui sont stockés dans Log Collection (le composant de stockage à long terme).  

Vous pouvez utiliser le plug-in {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} pour afficher le statut du journal, télécharger des journaux et configurer la règle de conservation des journaux. 

L'interface de ligne de commande propose différents types d'aide : une aide générale concernant l'interface de ligne de commande et les commandes prises en charge, une aide relative aux commandes pour savoir comment utiliser une commande, et une aide relative aux sous-commandes pour savoir comment utiliser une sous-commande d'une commande. 

Pour installer l'interface de ligne de commande {{site.data.keyword.loganalysisshort}} depuis le référentiel {{site.data.keyword.Bluemix_notm}}, procédez comme suit : 

1. Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. 

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)

2. Installez le plug-in {{site.data.keyword.loganalysisshort}}. Exécutez la commande suivante :

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. Vérifiez que le plug-in {{site.data.keyword.loganalysisshort}} est installé. 
  
    Par exemple, exécutez la commande suivante pour afficher la liste des plug-in qui sont installés : 
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    La sortie est similaire à la suivante :
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## Etape 4 : Définition des droits d'un utilisateur pour l'affichage des journaux 
{: #step4}

Pour contrôler les actions {{site.data.keyword.loganalysisshort}} qu'un utilisateur peut effectuer, vous pouvez affecter des rôles et des règles à un utilisateur.  

Dans {{site.data.keyword.Bluemix_notm}}, il existe deux types de droits de sécurité qui contrôlent les actions que les utilisateurs peuvent effectuer lorsqu'ils utilisent le service {{site.data.keyword.loganalysisshort}} : 

* Les rôles Cloud Foundry (CF) : vous attribuez un rôle CF à un utilisateur pour définir les droits dont cet utilisateur dispose pour afficher les journaux dans un espace. 
* Les rôles IAM : vous affectez une règle IAM à un utilisateur pour définir les droits dont cet utilisateur dispose pour afficher les journaux dans le domaine de compte et pour gérer les journaux qui sont stockés dans Log Collection.  


Procédez comme suit pour accorder à un utilisateur des droits permettant d'afficher les journaux dans un espace : 

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et lancez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique et leur statut sur le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam/iamuserinv.html#iamuserinv).

4. Sélectionnez **Accès Cloud Foundry**, puis sélectionnez l'organisation. 

    La liste des espaces disponibles dans cette organisation est affichée. 

5. Choisissez l'espace dans lequel vous avez mis à disposition le service {{site.data.keyword.loganalysisshort}}. Ensuite, dans le menu d'actions, sélectionnez **Editer un rôle d'espace**.

6. Sélectionnez *Auditeur*. 

    Vous pouvez sélectionner un ou plusieurs rôles d'espace. Les rôles suivants autorisent tous un utilisateur à afficher les journaux : *Responsable*, *Développeur* et *Auditeur*. 
	
7. Cliquez sur **Sauvegarder le rôle**.


Pour plus d'informations, voir [Octroi de droits](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).



## Etape 5 : Lancement de Kibana 
{: #step5}

Pour afficher et analyser les données de journal, vous devez accéder à Kibana dans la région de cloud publique dans laquelle les données de journal sont disponibles.  


Pour lancer Kibana dans la région Sud des Etats-Unis, ouvrez un navigateur Web et entrez l'URL suivante : 

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


Pour plus d'informations sur le lancement de Kibana dans d'autres régions, voir [Accès à Kibana depuis un navigateur Web](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

**Remarque :** lorsque vous lancez Kibana, si un message signale que le *jeton bearer n'est pas valide*, vérifiez vos droits dans l'espace. Ce message indique que votre ID utilisateur ne dispose pas des droits permettant d'afficher les journaux. 
    

## Etapes suivantes 
{: #next_steps}

Générez des journaux. Suivez l'un des tutoriels suivants : 

* [Analyse dans Kibana des journaux d'une application déployée dans un cluster Kubernetes](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    Ce tutoriel présente les étapes à suivre pour le scénario de bout en bout suivant : mettre à disposition un cluster, configurer le cluster pour l'envoi de journaux au service {{site.data.keyword.loganalysisshort}} dans {{site.data.keyword.Bluemix_notm}}, déployer une application dans le cluster, et utiliser Kibana afin d'afficher et de filtrer les journaux de conteneur pour ce cluster.      
    
* [Analyse des journaux dans Kibana pour une application Cloud Foundry](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    Ce tutoriel présente les étapes à suivre pour le scénario de bout en bout suivant : déployer une application Cloud Foundry Python, générer différents types de journal, et utiliser Kibana pour afficher, rechercher et analyser des journaux CF. 
   








