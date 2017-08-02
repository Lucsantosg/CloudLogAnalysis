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

# Interface de ligne de commande IBM Cloud Log Analysis
{: #logging_cli}

L'interface de ligne de commande {{site.data.keyword.loganalysislong}} est un plug-in qui permet de gérer les journaux des ressources de cloud s'exécutant dans un espace d'une
organisation {{site.data.keyword.Bluemix}}.
{: shortdesc}

**Prérequis**
* Avant d'exécuter les commandes de journalisation, connectez-vous à {{site.data.keyword.Bluemix_notm}} avec la commande `cf login`
pour générer un jeton d'accès {{site.data.keyword.Bluemix_short}} et authentifier votre session.

Pour savoir comment utiliser l'interface de ligne de commande {{site.data.keyword.loganalysisshort}},
voir [Gestion des journaux](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov).

<table>
  <caption>Commandes de gestion des journaux</caption>
  <tr>
    <th>Commande</th>
    <th>Quant l'utiliser</th>
  </tr>
  <tr>
    <td>[cf logging](#base)</td>
    <td>Utilisez cette commande pour obtenir des informations sur l'interface de ligne de commande, comme la version ou la liste des commandes.</td>
  </tr>
  <tr>
    <td>[cf logging auth](#auth)</td>
    <td>Utilisez cette commande pour obtenir le jeton de journalisation que vous pouvez utiliser pour envoyer des journaux au service {{site.data.keyword.loganalysisshort}}.</td>
  </tr>
  <tr>
    <td>[cf logging delete](#delete)</td>
    <td>Utilisez cette commande pour supprimer des journaux stockés dans la collecte des journaux.</td>
  </tr>
  <tr>
    <td>[cf logging download (Beta)](#download)</td>
    <td>Utilisez cette commande pour télécharger des journaux de la collecte des journaux vers un fichier local ou pour diriger des journaux vers un autre programme comme une pile ELK. </td>
  </tr>
  <tr>
    <td>[cf logging help](#help)</td>
    <td>Utilisez cette commande pour obtenir de l'aide au sujet de l'utilisation de l'interface de ligne de commande ainsi qu'une liste de toutes les commandes.</td>
  </tr>
  <tr>
    <td>[cf logging option](#option)</td>
    <td>Utilisez cette commande pour afficher ou définir la durée de conservation des journaux disponibles dans un compte ou un espace {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  <tr>
    <td>[cf logging session create (Beta)](#session_create)</td>
    <td>Utilisez cette commande pour créer une nouvelle session.</td>
  <tr>
  <tr>
    <td>[cf logging session delete (Beta)](#session_delete)</td>
    <td>Utilisez cette commande pour supprimer une session.</td>
  <tr>  
  <tr>
    <td>[cf logging session list (Beta)](#session_list)</td>
    <td>Utilisez cette commande pour afficher une liste des sessions actives et de leurs ID.</td>
  <tr>  
  <tr>
    <td>[cf logging session show (Beta)](#session_show)</td>
    <td>Utilisez cette commande pour afficher l'état d'une session unique.</td>
  <tr>  
  <tr>
    <td>[cf logging status](#status)</td>
    <td>Utilisez cette commande pour obtenir des informations sur les journaux collectés dans un compte ou un espace {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  </table>


## cf logging
{: #base}

Fournit des informations sur la version de l'interface de ligne de commande et sur son mode d'utilisation.

```
cf logging [parameters]
```
{: codeblock}

**Paramètres**

<dl>
<dt>--help, -h</dt>
<dd>Définissez ce paramètre pour afficher la liste des commandes ou pour obtenir de l'aide sur une commande.
</dd>

<dt>--version, -v</dt>
<dd>Définissez ce paramètre pour imprimer la version de l'interface de ligne de commande.</dd>
</dl>

**Exemples**

Pour obtenir la liste des commandes, exécutez la commande suivante :

```
cf logging --help
```
{: codeblock}

Pour obtenir la version de l'interface de ligne de commande, exécutez la commande suivante :

```
cf logging --version
```
{: codeblock}


## cf logging auth
{: #auth}

Renvoie un jeton de journalisation que vous pouvez utiliser pour envoyer des journaux au service {{site.data.keyword.loganalysisshort}}. 

**Remarque :** le jeton n'expire pas.

```
cf logging auth
```
{: codeblock}

**renvoie**

<dl>
  <dt>Jeton de journalisation</dt>
  <dd>Par exemple, `jec8BmipiEZc`.
  </dd>
  
  <dt>ID d'organisation</dt>
  <dd>Identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}} où vous êtes connecté.
  </dd>
  
  <dt>ID espace</dt>
  <dd>Identificateur global unique de l'espace dans l'organisation où vous êtes connecté.
  </dd>
</dl>

## cf logging delete
{: #delete}

Supprime les journaux stockés dans la collecte de journaux.

```
cf logging delete [parameters]
```
{: codeblock}

**Paramètres**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Facultatif) Définit la date de début en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*, par exemple `2006-01-02`. <br>La valeur par défaut est définie sur
les deux semaines précédentes.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Facultatif) Définit la date de fin en UTC (Universal Coordinated Time) : *AAAA-MM-JJ* <br>Le format UTC de la date est **AAAA-MM-JJ**,
par exemple `2006-01-02`. <br>La valeur par défaut est définie sur la date en cours.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Facultatif) Définit le type de journal. <br>Par exemple, *syslog* est un type de journal. <br>La valeur par défaut est définie sur **\***. <br>Vous
pouvez spécifier plusieurs types de journaux en séparant chaque type par une virgule, par exemple **log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Facultatif) Définit l'étendue des informations de journal fournies au niveau de compte. <br>Si ce paramètre n'est pas spécifié, la valeur par défaut est définie pour fournir des
informations de journal sur l'espace en cours uniquement.
  </dd>
</dl>

**Exemple**

Pour supprimer les journaux du type *linux_syslog* pour le 25 mai 2017, exécutez la commande suivante :
```
cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: codeblock}



## cf logging download (Beta)
{: #download}

Télécharge les journaux de Log Collection vers un fichier local ou dirige les journaux vers un autre programme, tel qu'une pile Elastic. 

**Remarque :** Pour télécharger les fichiers, vous devez d'abord créer une session. Une session définit quels journaux doivent être téléchargés en fonction de la plage
de dates, du type de journal et du type de compte. Les journaux sont téléchargés dans le contexte d'une session. Pour plus d'informations, voir [cf logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_create).

```
cf logging download [parameters] [arguments]
```
{: codeblock}

**Paramètres**

<dl>
<dt>--output value, -o value</dt>
<dd>(Facultatif) Définit le chemin et le nom du fichier de sortie local où les journaux sont téléchargés. <br>La valeur par défaut est un trait d'union (-). <br>Définissez ce
paramètre sur la valeur par défaut pour que les journaux soient générés dans la sortie standard.</dd>
</dl>

**Arguments**

<dl>
<dt>session_ID</dt>
<dd>Défini sur la valeur de l'ID de session que vous obtenez lorsque vous exécutez la commande `cf logging session create`. Cette valeur indique quelle session utiliser lors du
téléchargement des journaux. <br>**Remarque :** la commande `cf logging session create` fournit les paramètres qui contrôlent quels journaux sont
téléchargés. </dd>
</dl>

**Remarque :** si vous exécutez à nouveau la même commande une fois que le téléchargement est terminé, cela n'aura aucun effet. Pour télécharger à nouveau les mêmes
données, vous devez utiliser un fichier différent ou une session différente.

**Exemples**

Pour télécharger les journaux dans un fichier appelé mylogs.gz, exécutez la commande suivante :

```
cf logging download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

Pour télécharger des journaux dans votre pile Elastic, exécutez la commande suivante :

```
cf logging download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
```
{: screen}

Le fichier suivant est un exemple de fichier logstash.conf :

```
input {
  stdin {
    codec => json_lines {}
  }
}
output {
  elasticsearch {
    hosts => [ "127.0.0.1:9200" ]
  }
}
```
{: screen}


## cf logging help
{: #help}

Fournit des informations sur le mode d'utilisation d'une commande.

```
cf logging help [parameters]
```
{: codeblock}

**Paramètres**

<dl>
<dt>Commande</dt>
<dd>Définissez le nom de la commande pour laquelle vous souhaitez obtenir de l'aide.
</dd>
</dl>


**Exemples**

Pour obtenir de l'aide sur la façon dont vous pouvez exécuter la commande pour afficher l'état des journaux, exécutez la commande suivante :

```
cf logging help status
```
{: codeblock}


## cf logging option
{: #option}

Affiche ou change la durée de conservation des journaux disponibles dans un compte ou un espace {{site.data.keyword.Bluemix_notm}}. 

* La durée est définie en nombre de jours.
* La valeur par défaut est **-1**. 

**Remarque :** par défaut, tous les journaux sont stockés. Vous devez les supprimer manuellement à l'aide de la commande **delete**. Définissez une règle de conservation pour supprimer les journaux automatiquement. 

```
cf logging option [parameters]
```
{: codeblock}

**Paramètres**

<dl>
<dt>--retention value, -r value</dt>
<dd>(Facultatif) Définit le nombre de jours de conservation. <br> La valeur par défaut est de 30 jours.</dd>

<dt>--at-account-level, -a </dt>
  <dd>(Facultatif) Définit l'étendue du niveau de compte. <br>**Remarque :** Définissez cette valeur pour obtenir des informations relatives à un compte. <br>Si ce paramètre
n'est pas spécifié, la valeur par défaut est *30* pour l'espace en cours, c'est-à-dire l'espace auquel vous vous êtes connecté à l'aide de la commande `cf login`.
  </dd>
</dl>

**Exemples**

Pour afficher la durée de conservation en cours pour l'espace où vous êtes connecté, exécutez la commande suivante :

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


Pour modifier la durée de conservation à 25 jours pour l'espace où vous êtes connecté, exécutez la commande suivante :

```
cf logging option -r 25
```
{: codeblock}

La sortie est :

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        25 |
+--------------------------------------+-----------+
```
{: screen}


## cf logging session create (Beta)
{: #session_create}

Crée une nouvelle session.

**Remarque :** vous pouvez avoir jusqu'à 30 sessions simultanées dans un espace. La session est créée pour un utilisateur. Les sessions ne peuvent pas être partagées
entre les utilisateurs dans un espace.

```
cf logging session create [parameters]
```
{: codeblock}

**Paramètres**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Facultatif) Définit la date de début en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*, par exemple `2006-01-02`. <br>La valeur par défaut correspond aux
deux semaines précédant la date du jour.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Facultatif)  Définit la date de fin en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*, par exemple `2006-01-02`. <br>La valeur par défaut est définie sur la
date en cours.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Facultatif) Définit le type de journal. <br>Par exemple, *syslog* est un type de journal. <br>La valeur par défaut est un astérisque (*). <br>Vous pouvez spécifier plusieurs types de journaux en séparant chacun d'eux par une virgule, par exemple *log_type_1,log_type_2,log_type_3*. </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Facultatif) Définit l'étendue du niveau de compte. <br>**Remarque :** Définissez cette valeur pour obtenir des informations relatives à un compte. <br>Si ce paramètre
n'est pas spécifié, la valeur par défaut est uniquement définie sur l'espace en cours, à savoir l'espace sur lequel vous vous êtes connecté à l'aide de la commande `cf login`.
  </dd>
</dl>

**Valeurs renvoyées**

<dl>
<dt>Access-Time</dt>
<dd>Horodatage indiquant quand la session a été utilisée pour la dernière fois.</dd>

<dt>Create-Time</dt>
<dd>Horodatage correspondant à la date et à l'heure de création de la session.</dd>

<dt>Date-Range</dt>
<dd>Indique les dates utilisées pour filtrer les journaux. Les journaux identifiés à l'intérieur de la plage de dates peuvent être gérés via la session.</dd>

<dt>ID</dt>
<dd>ID de session.</dd>

<dt>Space</dt>
<dd>ID de l'espace où la session est active.</dd>

<dt>Type-Account</dt>
<dd>Types de journaux qui sont téléchargés via la session.</dd>

<dt>Username</dt>
<dd>ID {{site.data.keyword.IBM_notm}} de l'utilisateur qui a créé la session.</dd>
</dl>


**Exemple**

Pour créer une session incluant les journaux compris entre le 20 mai 2017 et le 26 mai 2017 pour un type de journal *log*, exécutez la commande suivante :

```
cf logging session create -s 2017-05-20 -e 2017-05-26 -t log
```
{: screen}


## cf logging session delete (Beta)
{: #session_delete}

Supprime une session, spécifiée par l'ID de session.

```
cf logging session delete [arguments]
```
{: codeblock}

**Arguments**

<dl>
<dt>session ID</dt>
<dd>ID de la session que vous souhaitez supprimer. <br>Vous pouvez utiliser la commande `cf logging session list` pour obtenir tous les ID des sessions actives.</dd>
</dl>

**Exemple**

Pour supprimer une session avec l'ID de session *cI6hvAa0KR_tyhjxZZz9Uw==*, exécutez la commande suivante :

```
cf logging session delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## cf logging session list (Beta)
{: #session_list}

Affiche une liste des sessions actives et de leurs ID.

```
cf logging session list 
```
{: codeblock}

**Valeurs renvoyées**

<dl>
<dt>ID</dt>
<dd>ID de session.</dd>

<dt>SPACE</dt>
<dd>ID de l'espace où la session est active.</dd>

<dt>USERNAME</dt>
<dd>ID {{site.data.keyword.IBM_notm}} de l'utilisateur qui a créé la session.</dd>

<dt>CREATE-TIME</dt>
<dd>Horodatage correspondant à la date et à l'heure de création de la session.</dd>

<dt>ACCESS-TIME</dt>
<dd>Horodatage indiquant quand la session a été utilisée pour la dernière fois.</dd>
</dl>
 

## cf logging session show (Beta)
{: #session_show}

Affiche l'état d'une session unique.

```
cf logging session show [arguments]
```
{: codeblock}

**Arguments**

<dl>
<dt>session_ID</dt>
<dd>ID de la session active sur laquelle vous souhaitez obtenir des informations.</dd>
</dl>

**Valeurs renvoyées**

<dl>
<dt>Access-Time</dt>
<dd></dd>

<dt>Create-Time</dt>
<dd>Horodatage correspondant à la date et à l'heure de création de la session.</dd>

<dt>Date-Range</dt>
<dd>Indique les dates utilisées pour filtrer les journaux. Les journaux identifiés à l'intérieur de la plage de dates peuvent être gérés via la session.</dd>

<dt>ID</dt>
<dd>ID de session.</dd>

<dt>Space</dt>
<dd>ID de l'espace où la session est active.</dd>

<dt>Type-Account</dt>
<dd>Types de journaux qui sont téléchargés via la session.</dd>

<dt>Username</dt>
<dd>ID {{site.data.keyword.IBM_notm}} de l'utilisateur qui a créé la session.</dd>
</dl>

**Exemple**

Pour afficher les détails d'une session avec l'ID de session *cI6hvAa0KR_tyhjxZZz9Uw==*, exécutez la commande suivante :

```
cf logging session show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}


## cf logging status
{: #status}

Renvoie des informations sur les journaux qui sont collectés dans un compte ou dans un espace {{site.data.keyword.Bluemix_notm}}.

```
cf logging status [parameters]
```
{: codeblock}

**Paramètres**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Facultatif) Définit la date de début en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*, par exemple `2006-01-02`. <br>La valeur par défaut correspond aux
deux semaines précédant la date du jour.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Facultatif)  Définit la date de fin en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*, par exemple `2006-01-02`. <br>La valeur par défaut est définie sur la
date en cours.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Facultatif) Définit le type de journal. <br>Par exemple, *syslog* est un type de journal. <br>La valeur par défaut est un astérisque (*). <br>Vous pouvez spécifier plusieurs types de journaux en séparant chacun d'eux par une virgule, par exemple *log_type_1,log_type_2,log_type_3*. </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Facultatif) Définit l'étendue du niveau de compte. <br> **Remarque :** Définissez cette valeur pour obtenir des informations relatives à un compte. <br>Si ce paramètre
n'est pas spécifié, la valeur par défaut est uniquement définie sur l'espace en cours, à savoir l'espace sur lequel vous vous êtes connecté à l'aide de la commande `cf login`.
  </dd>
  
  <dt>--list-type-detail, -l</dt>
  <dd>(Facultatif) Définissez ce paramètre pour afficher le sous-total des types de journaux pour chaque jour.
  </dd>
</dl>

**Remarque :** la commande `cf logging status` génère uniquement un rapport sur les deux dernières semaines de journaux stockés dans la collecte de
journaux si aucune date de début et de fin n'est spécifiée.


