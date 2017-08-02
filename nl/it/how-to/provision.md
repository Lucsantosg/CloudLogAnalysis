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


# Provisioning del servizio Analisi di log
{: #provision}

Puoi eseguire il provisioning del servizio {{site.data.keyword.loganalysisshort}} dall'IU {{site.data.keyword.Bluemix}} o dalla riga di comando.
{:shortdesc}


## Provisioning dall'IU
{: #ui}

Completa la seguente procedura per eseguire il provisioning di un'istanza del servizio {{site.data.keyword.loganalysisshort}} in {{site.data.keyword.Bluemix_notm}}:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}.

    Il dashboard {{site.data.keyword.Bluemix_notm}} è disponibile in: [http://bluemix.net ![Icona di link esterno](../../../icons/launch-glyph.svg "Icona di link esterno")](http://bluemix.net "Icona di link esterno"){:new_window}.
    
	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.Bluemix_notm}}.

2. Fai clic su **Catalogo**. Viene aperto l'elenco dei servizi disponibili in {{site.data.keyword.Bluemix_notm}}.

3. Seleziona la categoria **DevOps** per filtrare l'elenco di servizi visualizzato.

4. Fai clic sul tile **Analisi di log**.

5. Seleziona un piano di servizio. Per impostazione predefinita, è impostato il piano **Lite**.

    Per ulteriori informazioni sui piani di servizio, vedi [Piani di servizio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
6. Fai clic su **Crea** per eseguire il provisioning del servizio {{site.data.keyword.loganalysisshort}} nello spazio {{site.data.keyword.Bluemix_notm}} in cui hai eseguito l'accesso.
  
 

## Provisioning dalla CLI
{: #cli}

Completa la seguente procedura per eseguire il provisioning di un'istanza del servizio {{site.data.keyword.loganalysisshort}} in{{site.data.keyword.Bluemix_notm}} tramite la riga di comando:

1. Installa la CLI CF (Cloud Foundry). Se la CLI CF è installata, continua con il passo successivo.

   Per ulteriori informazioni, vedi il documento relativo all'[installazione della CLI cf![Icona di link esterno](../../../icons/launch-glyph.svg "Icona di link esterno")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Icona di link esterno"){: new_window}. 
    
2. Accedi a una regione, organizzazione e spazio {{site.data.keyword.Bluemix_notm}}. 

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui questo comando:

    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Attieniti alle istruzioni. Immetti le tue credenziali {{site.data.keyword.Bluemix_notm}}, seleziona un'organizzazione e uno spazio.
	
3. Esegui il comando `cf create-service` per eseguire il provisioning di un'istanza.

    ```
	cf create-service nome_servizio piano_di_servizio nome_istanza_servizio
	```
	{: codeblock}
	
	Dove
	
	* nome_servizio è il nome del servizio, ossia **ibmLogAnalysis**.
	* piano_di_servizio è il nome del piano di servizio. Per un elenco dei piani, vedi [Piani di servizio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	* nome_istanza_servizio è il nome che vuoi usare per la nuova istanza del servizio che crei.
	
	Per ulteriori informazioni sul comando cf, vedi [cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service).

	Ad esempio, per creare un'istanza del servizio {{site.data.keyword.loganalysisshort}} con un piano gratuito, esegui il seguente comando:
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}
	
4. Verifica che il servizio venga creato correttamente. Esegui il seguente comando:

    ```	
	cf services
	```
	{: codeblock}
	
	L'output dell'esecuzione del comando si presenta così:
	
	```
    Richiamo dei servizi nell'organizzazione MyOrg / space MySpace come xxx@yyy.com in corso...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	{: screen}

	



