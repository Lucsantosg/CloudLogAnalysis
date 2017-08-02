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

# Envoi de données à l'aide du réexpéditeur Logstash à service partagé
{: #send_data_mt}

Pour envoyer des données de journal au service {{site.data.keyword.loganalysisshort}}, vous pouvez configurer un réexpéditeur Logstash à service partagé (mt-logstash-forwarder). {:shortdesc}

Pour envoyer des données de journal à la collecte de journaux, procédez comme suit :

## Etape 1 : obtenez le jeton de journalisation
{: #get_logging_auth_token}

Pour envoyer des données au service {{site.data.keyword.loganalysisshort}}, vous avez besoin :

* d'un ID {{site.data.keyword.IBM_notm}} : cet ID est requis pour se connecter à {{site.data.keyword.Bluemix_notm}}.
* d'un espace dans une organisation {{site.data.keyword.Bluemix_notm}} : cet espace est l'endroit où vous prévoyez d'envoyer et d'analyser les journaux.
* d'un jeton de journalisation pour envoyer les données. 

Procédez comme suit :

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Exécutez la commande `cf logging auth`. 

    ```
    cf logging auth
    ```
    {: codeblock}

    La commande renvoie les informations suivantes :
    
    * Le jeton de journalisation.
    * L'ID d'organisation : il s'agit de l'identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté. 
    * L'ID d'espace : identificateur global unique de l'espace dans l'organisation à laquelle vous êtes connecté. 
    
    Par exemple

    ```
    cf logging auth
    +-----------------+--------------------------------------+
    |      NAME       |                VALUE                 |
    +-----------------+--------------------------------------+
    | Access Token    | $(cf oauth-token|cut -d' ' -f2)      |
    | Logging Token   | oT98_bKsdfTz                         |
    | Organization Id | 98450123-6f1c-9999-96a3-0210fjyuwplt |
    | Space Id        | 93f54jh6-b5f5-46c9-9f0e-kfeutpldnbcf |
    +-----------------+--------------------------------------+
    ```
    {: screen}

Pour plus d'informations, voir [cf logging auth](/docs/services/CloudLogAnalysis/reference/logging_cli.html#auth).


## Etape 2 : Configurez le mt-logstash-forwarder
{: #configure_mt_logstash_forwarder}

Procédez comme suit pour configurer mt-logstash-forwarder dans l'environnement depuis lequel vous prévoyez d'envoyer des journaux au service {{site.data.keyword.loganalysisshort}} :

1.	Connectez-vous en tant que superutilisateur. 

    ```
    sudo -s
    ```
    {: codeblock}
    
2.	Installez le package NTP (Network Time Protocol) pour synchroniser l'heure des journaux. 

    Par exemple, pour un système Ubuntu, vérifiez si `timedatectl status` affiche *Network time on: yes*. Dans le cas affirmatif, votre système Ubuntu est déjà configuré pour utiliser ntp et vous pouvez sauter cette étape.
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    Effectuez les étapes suivantes pour installer ntp dans un système Ubuntu :

    1.	Exécutez la commande suivante pour mettre à jour les packages. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Exécutez la commande suivante pour installer le package ntp. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Exécutez la commande suivante pour installer le package ntpdate. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Exécutez la commande suivante pour arrêter le service 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Exécutez la commande suivante pour synchroniser l'horloge système. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        Le résultat confirme que l'heure est réglée, par exemple :
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Exécutez la commande suivante pour démarrer ntpd à nouveau. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        Le résultat confirme que le service démarre.

    7.	Exécutez la commande suivante pour activer le service ntpd pour démarrer automatiquement après une panne ou un réamorçage. 
    
        ```
        service ntp enable
        ```
        {: codeblock}
        
        Le résultat qui s'affiche est une liste des commandes qui peuvent être utilisées pour gérer le service ntpd, par exemple :
        
        ```
        Usage: /etc/init.d/ntpd {start|stop|status|restart|try-restart|force-reload}
        ```
        {: screen}

3. Ajoutez le référentiel du service {{site.data.keyword.loganalysisshort}} dans le gestionnaire de package du système. Exécutez la commande suivante :

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
    {: codeblock}

4. Installez et configurez mt-logstash-forwarder pour envoyer des journaux de votre environnement à la collecte de journaux. 

    1. Exécutez la commande suivante pour installer mt-logstash-forwarder :
    
        ```
        apt-get install mt-logstash-forwarder 
        ```
        {: codeblock}
        
    2. Créez le fichier de configuration mt-logstash-forwarder pour votre environnement. Ce fichier inclut des variables qui sont utilisées pour configurer mt logstash forwarder pour que le réexpéditeur pointe sur le service {{site.data.keyword.loganalysisshort}}.
    
       Editez le fichier `/etc/mt-logstash-forwarder/mt-lsf-config.sh`. Par exemple, vous pouvez utiliser l'éditeur vi :
               
       ```
       vi /etc/mt-logstash-forwarder/mt-lsf-config.sh
       ```
       {: codeblock}
        
       Pour que le réexpéditeur pointe sur le service {{site.data.keyword.loganalysisshort}}, ajoutez les variables suivantes au fichier **mt-lsf-config.sh** : 
         
       <table>
          <caption>Tableau 1. Liste des variables requises pour que le réexpéditeur pointe sur le service {{site.data.keyword.loganalysisshort}} dans une machine virtuelle </caption>
          <tr>
            <th>Nom de la variable</th>
            <th>Description</th>
          </tr>
          <tr>
            <td>LSF_INSTANCE_ID</td>
            <td>ID de votre machine virtuelle, par exemple *MyTestVM*. </td>
          </tr>
          <tr>
            <td>LSF_TARGET</td>
            <td>URL cible. Définissez la valeur **https://ingest.logging.ng.bluemix.net:9091**.</td>
          </tr>
          <tr>
            <td>LSF_TENANT_ID</td>
            <td>ID d'espace où le service {{site.data.keyword.loganalysisshort}} est prêt à collecter les journaux que vous envoyez dans {{site.data.keyword.Bluemix_notm}}. <br>Utilisez la valeur obtenue à l'étape 1.</td>
          </tr>
          <tr>
            <td>LSF_PASSWORD</td>
            <td>Jeton de journalisation. <br>Utilisez la valeur obtenue à l'étape 1.</td>
          </tr>
          <tr>
            <td>LSF_GROUP_ID</td>
            <td>Définissez cette valeur sur une balise personnalisée que vous pouvez définir pour regrouper des journaux connexes.</td>
          </tr>
       </table>
        
       Par exemple, recherchez dans l'exemple de fichier suivant un espace ayant l'ID *7d576e3b-170b-4fc2-a6c6-b7166fd57912* dans la région Royaume-Uni :
        
       ```
       # more mt-lsf-config.sh 
       LSF_INSTANCE_ID="myhelloapp"
       LSF_TARGET="ingest.logging.ng.bluemix.net:9091"
       LSF_TENANT_ID="7d576e3b-170b-4fc2-a6c6-b7166fd57912"
       LSF_PASSWORD="oT98_bKsdfTz"
       LSF_GROUP_ID="Group1"
       ```
       {: screen}
        
    3. Démarrez mt-logstash-forwarder. 
    
       ```
       service mt-logstash-forwarder start
       ```
       {: codeblock}
        
       Activez mt-logstash-forwarder pour démarrer automatiquement après une panne ou un réamorçage. 
        
       ```
       service mt-logstash-forwarder enable
       ```
       {: codeblock}
        
       **Astuce :** Pour redémarrer le service mt-logstash-forwarder, exécutez la commande suivante :
    
       ```
       service mt-logstash-forwarder restart
       ```
       {: codeblock}
        
        
Par défaut, le réexpéditeur assiste uniquement syslog. Vos journaux sont disponibles dans Kibana pour analyse.
        

## Etape 3 : spécifiez des fichiers journaux additionnels
{: #add_logs}

Par défaut, seul le fichier /var/log/syslog est contrôlé par le réexpéditeur. Vous pouvez ajouter des fichiers de configuration supplémentaires au répertoire `/etc/mt-logstash-forwarder/conf.d/syslog.conf/` afin que le réexpéditeur les contrôle également. 

Exécutez les étapes suivantes pour ajouter un fichier de configuration pour une application qui s'exécute dans votre environnement :

1.	Copiez le fichier `/etc/mt-logstash-forwarder/conf.d/syslog.conf`. 

    **Astuce :** N'éditez pas le fichier syslog.conf pour ajouter des fichiers journaux.
    
    Par exemple, dans un système Ubuntu, exécutez la commande suivante :
    
    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
        
2.	Avec un éditeur de texte, éditez le fichier *myapp.conf* et mettez à jour le fichier pour inclure les journaux d'application que vous souhaitez contrôler. Incluez le type de journal de chaque journal d'application. Supprimez les exemples qui ne sont pas utilisés.

3.	Redémarrez mt-logstash-forwarder. 

     Redémarrez le service mt-logstash-forwarder. Exécutez la commande suivante :
    
    ```
    service mt-logstash-forwarder restart
    ```
    {: codeblock}

**Exemple**

Pour inclure le stdout ou le stderr d'une application hello, redirigez stdout ou stderr vers un fichier journal. Créez un fichier de configuration de réexpéditeur pour l'application. Ensuite, redémarrez mt-logstash-forwarder.

1.	Copiez le fichier `/etc/mt-logstash-forwarder/conf.d/syslog.conf`. 

    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
    
2. Editez le fichier de configuration *myapp.conf*.

    Pour activer l'analyse JSON, définissez is_json sur true dans le fichier de configuration.
    
    ```
    {
    "files": [
         # other file configurations omitted...
            {
            "paths": [ "/var/log/myhelloapp.log" ],
            "fields": { "type": "helloapplog" },
            "is_json": true
            }
         ]
     }
     ```
     {: screen}
