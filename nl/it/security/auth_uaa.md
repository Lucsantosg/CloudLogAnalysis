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


# Ottenimento del token UAA
{: #auth_uaa}

Per gestire i log utilizzando la API {{site.data.keyword.loganalysisshort}}, devi utilizzare un token di autenticazione. Utilizza la CLI {{site.data.keyword.loganalysisshort}} per ottenere il token UAA. Il token ha un tempo di scadenza. 
{:shortdesc}

		
## Ottenimento del token UAA utilizzando la CLI Analisi dei log (plugin CF)
{: #uaa_cli}


Per ottenere il token di autorizzazione, completa la seguente procedura:

1. Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Scarica e installa la CLI {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Se la CLI è installata, continua con il passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Esegui il comando `bx cf oauth-token` per ottenere il token UAA {{site.data.keyword.Bluemix_notm}}.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	L'output restituisce il token UAA che devi usare per autenticare il tuo ID utente in tale spazio e organizzazione.
	

**Nota:** quando usi il token, rimuovi *Bearer* dal valore del token che passi in una chiamata API.
