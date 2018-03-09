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


# Octroi de droits
{: #grant_permissions}

Dans {{site.data.keyword.Bluemix}}, vous pouvez affecter un ou plusieurs rôles à des utilisateurs. Ces rôles définissent quelles tâches sont activées pour que cet utilisateur puisse se servir du service {{site.data.keyword.loganalysisshort}}. 
{:shortdesc}



## Affectation d'une règle IAM à un utilisateur dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}
{: #grant_permissions_ui_account}

Afin d'accorder des droits à un utilisateur pour qu'il puisse afficher et gérer les journaux de compte, vous devez ajouter une règle pour cet utilisateur qui décrit les actions qu'il peut effectuer avec le service {{site.data.keyword.loganalysisshort}} sur le compte. Seuls les propriétaires de compte peuvent affecter des règles individuelles à des utilisateurs.

Dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit pour accorder à un utilisateur des droits lui permettant d'utiliser le service {{site.data.keyword.loganalysisshort}} :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et lancez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique et leur statut sur le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam/iamuserinv.html#iamuserinv).

4. Dans la section **Règles d'accès**, cliquez sur **Affecter des règles de service**, puis cliquez sur **Affecter l'accès aux ressources**. 

    La fenêtre *Affecter l'accès à la ressource à** s'ouvre. 

5. Entrez les informations concernant la règle. Le tableau ci-dessous répertorie les zones requises pour définir une règle.  

    <table>
	  <caption>Liste des zones de configuration d'une règle IAM.</caption>
	  <tr>
	    <th>Zone</th>
		<th>Valeur</th>
	  </tr>
	  <tr>
	    <td>Services</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>Régions</td>
		<td>Vous pouvez spécifier les régions dans lesquelles l'utilisateur disposera des droits permettant d'utiliser les journaux. Sélectionnez ou une plusieurs régions individuellement, ou sélectionnez **Toutes les régions en cours** pour accorder l'accès à toutes les régions. </td>
	  </tr>
	  <tr>
	    <td>Instance de service</td>
		<td>Sélectionnez *Toutes les instances de service*.</td>
	  </tr>
	  <tr>
	    <td>Rôles</td>
		<td>Sélectionnez un ou plusieurs rôles IAM. <br>Les rôles valides sont *administrateur*, *opérateur*, *éditeur* et *afficheur*. <br>Pour plus d'informations sur les actions autorisées pour chaque rôle, voir [Rôle IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).
		</td>
	  </tr>
     </table>
	
6. Cliquez sur **Affecter une règle**.
	
La règle que vous configurez est applicable aux régions sélectionnées. 

## Affectation d'une règle IAM à un utilisateur via la ligne de commande
{: #grant_permissions_commandline}

Pour accorder à un utilisateur les droits permettant d'afficher et de gérer les journaux de compte, vous devez lui affecter un rôle IAM. Pour plus d'informations sur les rôles IAM et les tâches dans chaque rôle permettant d'utiliser le service {{site.data.keyword.loganalysisshort}}, voir [Rôles IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).

Cette opération ne peut être effectuée que par le propriétaire de compte.

Procédez comme suit pour accorder à un utilisateur le droit permettant d'afficher les journaux de compte via la ligne de commande :

1. Obtenez l'ID de compte. 

    Pour obtenir l'ID de compte, exécutez la commande suivante :

    ```
	bx iam accounts
	```
    {: codeblock}	

	La liste des comptes avec leur identificateur global unique s'affiche.
	
	Exportez l'ID du compte pour lequel vous prévoyez d'accorder des droits à un utilisateur dans une variable de shell telle que `$acct_id`, par exemple :
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. Obtenez l'ID {{site.data.keyword.Bluemix_notm}} de l'utilisateur auquel vous voulez accorder des droits.

    1. Affichez les utilisateurs associés au compte. Exécutez la commande suivante :
	
	    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. Obtenez l'identificateur global unique de l'utilisateur. **Remarque :** cette étape doit être effectuée par l'utilisateur auquel vous prévoyez d'accorder des droits.
	
	    Par exemple, demandez à l'utilisateur d'exécuter les commandes suivantes pour obtenir son ID utilisateur :
		
		Obtenez le jeton IAM. Pour plus d'informations, voir [Obtention du jeton IAM via l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

        Prenez les données situées entre les deux premiers points dans le jeton IAM. Exportez les données dans une variable de shell telle que `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Par exemple, exécutez la commande ci-dessous pour obtenir l'ID utilisateur. Dans l'exemple, cette commande utilise jq pour décoder les informations que contient le texte JSON formaté :
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		La sortie de cette commande est la suivante :
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Envoyez l'ID utilisateur au propriétaire du compte.
		
	3. Exportez l'ID utilisateur dans une variable de shell telle que `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Invitez l'utilisateur sur le compte s'il n'en est pas déjà membre. Pour plus d'informations, voir [Invitation d'utilisateurs](/docs/iam/iamuserinv.html#iamuserinv).

    Par exemple, exécutez la commande suivante pour inviter l'utilisateur xxx@yyy.com sur le compte zzz@ggg.com :
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Créez un nom de fichier de règle. 

    Par exemple, utilisez le modèle suivant pour accorder des droits d'affichage dans la région Sud des Etats-Unis :
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-log-analysis",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nommez le fichier de règle : `policy.json`
	
5. Obtenez le jeton IAM pour votre ID utilisateur.

    Pour plus d'informations, voir [Obtention du jeton IAM via l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

    Exportez le jeton IAM dans une variable de shell telle que `$iam_token`, par exemple :
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Accordez à l'utilisateur des droits lui permettant d'utiliser le service {{site.data.keyword.loganalysisshort}}. 

   Exécutez la commande cURL suivante pour accorder des droits dans la région Sud des Etats-Unis :
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Exécutez la commande cURL suivante pour accorder des droits dans la région Royaume-Uni :
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
Une fois les droits accordés à un utilisateur, ce dernier peut se connecter à {{site.data.keyword.Bluemix_notm}} et afficher les journaux au niveau du compte.



## Octroi à un utilisateur des droits permettant d'afficher les journaux d'espace dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}
{: #grant_permissions_ui_space}

Pour accorder à un utilisateur des droits permettant d'afficher les journaux dans un espace, vous devez lui affecter un rôle Cloud Foundry qui décrit les actions qu'il peut effectuer avec le service {{site.data.keyword.loganalysisshort}} dans l'espace.

Pour accorder à un utilisateur des droits permettant d'utiliser le service {{site.data.keyword.loganalysisshort}}, procédez comme suit :

1. Connectez-vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et démarrez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam/iamuserinv.html#iamuserinv).

4. Sélectionnez **Accès Cloud Foundry**, puis sélectionnez l'organisation.

    La liste des espaces disponibles dans cette organisation est affichée.

5. Choisissez un espace. Ensuite, dans le menu d'actions, sélectionnez **Editer un rôle d'espace**.

6. Sélectionnez un ou plusieurs rôles d'espace. Les rôles valides sont : *Responsable*, *Développeur* et *Auditeur*.
	
7. Cliquez sur **Sauvegarder le rôle**.




