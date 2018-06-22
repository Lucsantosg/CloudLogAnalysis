---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurazione della politica di conservazione dei log
{: #configuring_retention_policy}

Per impostazione predefinita, la politica di conservazione è disabilitata e i log vengono conservati indefinitamente. Utilizza il comando **bx logging option-update** per modificare la politica di conservazione.
{:shortdesc}

Puoi utilizzare il comando **bx logging option-show** per visualizzare la politica di conservazione che definisce il numero massimo di giorni per cui i log vengono conservati nella Raccolta dei log. 

Quando imposti una politica di conservazione, allo scadere del periodo di conservazione i log vengono automaticamente eliminati.


## Disabilitazione della politica di conservazione dei log per un account
{: #disable_retention_policy_acc}

Quando disabiliti la politica di conservazione, vengono conservati tutti i log. 

Completa la seguente procedura per disabilitare una politica di conservazione:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Ottieni l'ID account.

    Per ulteriori informazioni, vedi [Come ottengo il GUID di un account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Imposta il periodo di conservazione su **-1** per disabilitarlo. Esegui il comando:

    ```
    bx logging option-update -r account -i AccountID -e RETENTION_VALUE
	```
    {: codeblock}
	
	RETENTION_VALUE è un numero che definisce la quantità di giorni.
    
**Esempio**
    
Ad esempio, per disabilitare il periodo di conservazione per un account con ID *12345677fgh436902a3*, esegui questo comando:

```
bx logging option-update -r account -i 12345677fgh436902a3 -e -1
```
{: codeblock}


## Disabilitazione della politica di conservazione dei log per uno spazio
{: #disable_retention_policy_space}

Quando disabiliti la politica di conservazione, vengono conservati tutti i log.  

Completa la seguente procedura per disabilitare una politica di conservazione:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Imposta il periodo di conservazione su **-1** per disabilitare il periodo di conservazione. Esegui il comando:

    ```
    bx logging option-show -e RETENTION_VALUE
	```
    {: codeblock}
	
	RETENTION_VALUE è un numero che definisce la quantità di giorni.
    
**Esempio**
    
Ad esempio, per disabilitare il periodo di conservazione per uno spazio con ID *d35da1e3-b345-475f-8502-cfgh436902a3*, esegui il seguente comando:

```
bx logging option-update -e -1
```
{: codeblock}


## Controllo della politica di conservazione dei log per un account
{: #check_retention_policy_acc}

Per ottenere il periodo di conservazione impostato per un account, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Ottieni l'ID account.

    Per ulteriori informazioni, vedi [Come ottengo il GUID di un account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Ottieni il periodo di conservazione. Esegui il comando:

    ```
    bx logging option-show -r account -i AccountID
    ```
    {: codeblock}

    L'output è:

    ```
    bx logging option-show -r account -i kjskdsjfksjdflkjdsfbbd06461b066
    Showing log options of resource: kjskdsjfksjdflkjdsfbbd06461b066 ...

    Resource ID                              Retention   
    a:kjskdsjfksjdflkjdsfbbd06461b066       30   
	```
    {: screen}
	
## Controllo della politica di conservazione dei log per uno spazio
{: #check_retention_policy_space}

Per ottenere il periodo di conservazione impostato per uno spazio, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Ottieni il periodo di conservazione. Esegui il comando:

    ```
    bx logging option-show
    ```
    {: codeblock}

    L'output è:

    ```
    bx logging option-show
    Showing log options of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    SpaceId                                Retention   
    12345678-1234-2edr-a9de-378620d6fab5   30   
	```
    {: screen}
    


## Impostazione di una politica di conservazione dei log a livello di account
{: #set_retention_policy_acc}

Completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Ottieni l'ID account.

    Per ulteriori informazioni, vedi [Come ottengo il GUID di un account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Imposta il periodo di conservazione. Esegui il comando:

    ```
    bx logging option-update -r account -i AccountID -e RETENTION_VALUE
    ```
    {: codeblock}
    
    dove *RETENTION_VALUE* è un numero intero che definisce il numero di giorni per cui vuoi conservare i log. 
    
    
**Esempio**
    
Ad esempio, per conservare qualsiasi tipo di log nel tuo account soltanto per 15 giorni, esegui il seguente comando:

```
bx logging option-update -r account -i AccountID -e 15
```
{: codeblock}



## Impostazione della politica di conservazione dei log per uno spazio
{: #set_retention_policy_space}

Per vedere il periodo di conservazione per uno spazio, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Imposta il periodo di conservazione. Esegui il comando:

    ```
    bx logging option-update -e RETENTION_VALUE
    ```
    {: codeblock}
    
    dove *RETENTION_VALUE* è un numero intero che definisce il numero di giorni per cui vuoi conservare i log.
    
    
**Esempio**
    
Ad esempio, per conservare i log disponibili in un spazio per un anno, esegui il seguente comando:

```
bx logging option-update -e 365
```
{: codeblock}




