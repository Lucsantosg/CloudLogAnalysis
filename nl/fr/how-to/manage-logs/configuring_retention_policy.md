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

# Configuration de la règle de conservation des journaux
{: #configuring_retention_policy}

Utilisez la commande **cf logging option** pour afficher et configurer la règle de conservation qui définit le nombre maximal de jours pendant lesquels les journaux sont
conservés dans Collecte des journaux. Par défaut, les journaux sont conservés pendant 30 jours. Une fois que la durée de conservation a expiré, les journaux sont supprimés automatiquement. Par
défaut, la règle de conservation est désactivée.
{:shortdesc}

Vous pouvez définir différentes règles de conservation dans le compte, notamment une règle de compte globale et des règles d'espace individuelles. La règle de conservation que vous avez
définie au niveau du compte définit le nombre de jours pendant lesquels vous pouvez conserver les journaux. Si vous définissez la règle de conservation d'un espace sur une durée supérieure à la
durée du niveau de compte, la règle appliquée est la dernière règle configurée pour cet espace. 


## Désactivation de la règle de conservation des journaux pour un espace
{: #disable_retention_policy_space}

Effectuez les étapes suivantes pour désactiver une règle de conservation :

1. Connectez-vous à l'espace, à l'organisation et à la région {{site.data.keyword.Bluemix_notm}} où vous souhaitez définir une règle de conservation des journaux. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Définissez la durée de conservation sur **-1** pour la désactiver. Exécutez la commande suivante :

    ```
    cf logging option -r -1
    ```
    {: codeblock}
    
**Exemple**
    
Par exemple, pour désactiver la durée de conservation d'un espace avec l'ID *d35da1e3-b345-475f-8502-cfgh436902a3*, exécutez la commande suivante :

```
cf logging option -r -1
```
{: codeblock}

La sortie est :

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen} 



## Vérification de la règle de conservation des journaux d'un espace
{: #check_retention_policy_space}

Pour obtenir la durée de conservation définie pour un espace {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez-vous à l'espace, à l'organisation et à la région {{site.data.keyword.Bluemix_notm}} où vous souhaitez définir une règle de conservation des journaux. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenez la durée de conservation. Exécutez la commande suivante :

    ```
    cf logging option
    ```
    {: codeblock}

    La sortie est :

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Vérification de la règle de conservation des journaux de tous les espaces d'un compte
{: #check_retention_policy_account}

Pour obtenir la durée de conservation définie pour chaque espace {{site.data.keyword.Bluemix_notm}} d'un compte, procédez comme suit :

1. Connectez-vous à l'espace, à l'organisation et à la région {{site.data.keyword.Bluemix_notm}} où vous souhaitez définir une règle de conservation des journaux. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenez la durée de conservation de chaque espace du compte. Exécutez la commande suivante :

    ```
    cf logging option -a
    ```
    {: codeblock}

    La sortie est :

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
    

## Définition de la règle de conservation des journaux d'un niveau de compte
{: #set_retention_policy_space}

Pour afficher la durée de conservation d'un compte {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez-vous à l'espace, à l'organisation et à la région {{site.data.keyword.Bluemix_notm}} où vous souhaitez définir une règle de conservation des journaux. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Définissez la durée de conservation. Exécutez la commande suivante :

    ```
    cf logging option -r *Number_of_days* - a
    ```
    {: codeblock}
    
    où *Number_of_days* est un nombre entier qui définit le nombre de jours pendant lesquels vous souhaitez conserver les journaux. 
    
    
**Exemple**
    
Par exemple, pour conserver un type de journal spécifique dans votre compte pendant seulement 15 jours, exécutez la commande suivante :

```
cf logging option -r 15 -a
```
{: codeblock}

La sortie affiche une entrée pour chaque espace du compte, y compris des informations sur la durée de conservation :

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

## Définition de la règle de conservation des journaux pour un espace
{: #set_retention_policy_account}

Pour afficher la durée de conservation d'un espace {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez-vous à l'espace, à l'organisation et à la région {{site.data.keyword.Bluemix_notm}} où vous souhaitez définir une règle de conservation des journaux. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Définissez la durée de conservation. Exécutez la commande suivante :

    ```
    cf logging option -r *Number_of_days*
    ```
    {: codeblock}
    
    où *Number_of_days* est un nombre entier qui définit le nombre de jours pendant lesquels vous souhaitez conserver les journaux.
    
    
**Exemple**
    
Par exemple, pour conserver les journaux disponibles dans un espace pendant un an, exécutez la commande suivante :

```
cf logging option -r 365
```
{: codeblock}

La sortie est :

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |       365 |
+--------------------------------------+-----------+
```
{: screen}


