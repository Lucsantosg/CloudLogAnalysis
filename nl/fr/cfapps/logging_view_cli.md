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


# Analyse des journaux CF depuis l'interface de ligne de commande
{: #analyzing_logs_cli}

Dans {{site.data.keyword.Bluemix}}, vous pouvez afficher, filtrer et analyser des journaux depuis l'interface de ligne de commande. 
{:shortdesc}

Pour analyser des journaux d'application Cloud Foundry (CF), utilisez les commandes suivantes : `cf logs`.
Pour plus d'informations, voir [Analyse de journaux d'application CF depuis l'interface de ligne de commande](/docs/services/CloudLogAnalysis/logging_view_cli.html#analyzing_cf_logs_cli).


## Analyse des journaux d'application CF depuis l'interface de ligne de commande
{: #analyzing_cf_logs_cli}

Utilisez la commande **cf logs** pour afficher des journaux depuis une application Cloud Foundry et depuis les composants système qui interagissent avec cette application lorsque vous déployez l'application dans {{site.data.keyword.Bluemix_notm}}. La commande **cf logs** affiche les flux de journalisation de sortie standard et d'erreur standard d'une application Cloud Foundry.

Pour afficher les journaux qui vous intéressent ou exclure le contenu que vous ne voulez pas afficher, vous pouvez utiliser la commande **cf logs** avec des options de filtrage telles que **cut** et **grep** dans l'interface de ligne de commande cf :

* Pour afficher les journaux d'une application Cloud Foundry, voir [Affichage du journal d'une application Cloud Foundry](logging_view_cli.html#full_log_cli).
* Pour afficher les derniers enregistrements de journal d'une application Cloud Foundry, voir [Affichage des dernières entrées de journal d'une application Cloud Foundry](logging_view_cli.html#tailing_log_cli).
* Pour afficher les enregistrements de journal d'une application Cloud Foundry pour une période donnée, voir [Affichage d'une section d'un journal](logging_view_cli.html#partial_log_cli).
* Pour afficher les entrées des journaux d'une application Cloud Foundry qui contiennent des mots clés spécifiques, voir [Affichage d'entrées de journal contenant certains mots clés](logging_view_cli.html#partial_by_keyword_log_cli).


### Affichage du journal d'une application Cloud Foundry
{: #full_log_cli}

Pour afficher tous les journaux disponibles pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix_notm}}.

2. Depuis la ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

   <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var></code></pre>
   
   
### Affichage des dernières entrées de journal d'une application Cloud Foundry
{: #tailing_log_cli}

Pour afficher les derniers journaux disponibles pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix_notm}}.

2. Depuis la ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

     <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Astuce :</span> lorsque vous exécutez la commande <span class="keyword cmdname">cf push</span> ou <span class="keyword cmdname">cf start</span> dans une seule fenêtre de ligne de commande, vous pouvez entrer <samp class="ph codeph">cf logs nom_app --recent</samp> dans une autre fenêtre de ligne de commande pour afficher les journaux en temps réel. </div>


### Affichage d'une section d'un journal Cloud Foundry
{: #partial_log_cli}

Pour afficher une partie des journaux disponibles pour une application Cloud Foundry pour une période donnée, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix_notm}}.

2. Depuis la ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

    <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Pour plus d'informations sur l'option **cut**, entrez **cut --help**.


### Affichage d'entrées de journal contenant certains mots clés
{: #partial_by_keyword_log_cli}

Pour afficher les entrées de journal contenant certains mots clés pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix}}.

2. Depuis la ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

    <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent | grep '<var class="keyword varname">mot clé</var>'</code></pre>
    

Par exemple, pour afficher les entrées de journal contenant le mot clé **APP**, utilisez la commande suivante :

<pre class="pre screen"><code>cf logs nom_app --recent | grep '\[App' </code></pre>

Pour plus d'informations sur l'option **grep**, entrez **grep --help**.


### Journaux des applications Cloud Foundry
{: #cf_app_logs_cli}

Les journaux suivants sont disponibles pour une application Cloud Foundry après que vous l'avez déployée dans {{site.data.keyword.Bluemix}} :

**buildpack.log**

Ce fichier journal enregistre des événements d'information à granularité fine pour le débogage. Vous pouvez l'utiliser pour identifier les problèmes liés à l'exécution du pack de construction.

Pour générer des données dans le fichier *buildpack.log*, vous devez activer le traçage de pack de construction via la commande : `cf set-env nom_application JBP_LOG_LEVEL DEBUG`
   
Pour consulter ce journal, entrez la commande suivante : `cf files nom_application app/.buildpack-diagnostics/buildpack.log`


**staging_task.log**

Ce fichier journal enregistre des messages après les étapes principales de la tâche de constitution. Vous pouvez l'utiliser pour identifier les problèmes liés à la constitution.

Pour consulter ce journal, entrez la commande suivante : `cf files nom_application logs/staging_task.log`


**Remarque :** pour des informations sur l'activation de la journalisation des applications, voir [Débogage d'erreurs d'exécution](/docs/debug/index.html#debugging-runtime-errors).



