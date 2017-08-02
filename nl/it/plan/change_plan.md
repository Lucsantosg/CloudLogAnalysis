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


# Modifica del piano
{: #change_plan}

Puoi modificare il tuo piano del servizio {{site.data.keyword.loganalysisshort}} in {{site.data.keyword.Bluemix_notm}} nel dashboard del servizio o eseguendo il comando `cf update-service`. Puoi aggiornare o ridurre il tuo piano in qualsiasi momento.
{:shortdesc}

## Modifica del piano del servizio tramite la IU.
{: #change_plan_ui}

Per modificare il tuo piano del servizio in {{site.data.keyword.Bluemix_notm}} nel dashboard del servizio, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul servizio {{site.data.keyword.loganalysisshort}} dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Seleziona la scheda **Piano** nella IU {{site.data.keyword.Bluemix_notm}}.

    Vengono visualizzate le informazioni sul tuo piano corrente.
	
3. Seleziona un nuovo piano per aggiornare o ridurre il tuo piano. 

4. Fai clic su **Salva**.



## Modifica del piano del servizio tramite la CLI
{: #change_plan_cli}

Per modificare il tuo piano del servizio in Bluemix tramite la CLI, completa la seguente procedura:

1. Accedi a una regione, organizzazione e spazio {{site.data.keyword.Bluemix_notm}}. 

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui questo comando:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
	
2. Esegui il comando `cf services` per verificare il tuo piano corrente e per ottenere il nome del servizio {{site.data.keyword.loganalysisshort}} dall'elenco dei servizi disponibili nello spazio. 

    Il valore del campo **name** deve essere utilizzato per modificare il piano. 

    Ad esempio,
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Aggiorna o riduci il tuo piano. Esegui il comando `cf update-service`.
    
	```
	cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	dove 
	
	* *service_name* è il nome del tuo servizio. Puoi eseguire il comando `cf services` per ottenere il valore.
	* *new_plan* è il nome del piano.
	
	La seguente tabella elenca i diversi piani e i rispettivi valori supportati:
	
	<table>
	  <caption>Tabella 1. Elenco dei piani.</caption>
	  <tr>
	    <th>Piano</th>
	    <th>Nome</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>Raccolta dei log</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>Raccolta dei log con 2 GB/Ricerca al giorno</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>Raccolta dei log con 5 GB/Ricerca al giorno</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>Raccolta dei log con 10 GB/Ricerca al giorno</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	Ad esempio, per ridurre il tuo piano al piano *Lite*, esegui il seguente comando:
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifica che il nuovo piano è stato modificato. Esegui il comando `cf services`.

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






