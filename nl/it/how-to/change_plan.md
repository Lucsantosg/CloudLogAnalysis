---

copyright:
  years: 2017, 2018

lastupdated: "2018-03-15"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modifica del piano
{: #change_plan}

Puoi modificare il tuo piano di servizio {{site.data.keyword.loganalysisshort}} tramite l'interfaccia utente {{site.data.keyword.Bluemix_notm}} oppure eseguendo il comando `bx cf update-service`. Puoi aggiornare o ridurre il tuo piano in qualsiasi momento.
{:shortdesc}

## Modifica del piano di servizio tramite la IU.
{: #change_plan_ui}

Per modificare il piano di servizio nella IU {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}. 

2. Seleziona la regione, l'organizzazione e lo spazio in cui è disponibile il servizio {{site.data.keyword.loganalysisshort}}.  

3. Fai clic sull'istanza del servizio {{site.data.keyword.loganalysisshort}} dal {{site.data.keyword.Bluemix_notm}} *Dashboard*. 
    
4. Seleziona la scheda **Piano** nel dashboard {{site.data.keyword.loganalysisshort}}.

    Vengono visualizzate le informazioni sul tuo piano corrente.
	
5. Seleziona un nuovo piano per aggiornare o ridurre il tuo piano. 

6. Fai clic su **Salva**.




## Modifica del piano di servizio tramite la CLI
{: #change_plan_cli}

Per modificare il tuo piano di servizio in Bluemix tramite la CLI, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Esegui il comando `bx service list` per controllare il tuo piano attuale e per ottenere il nome del servizio {{site.data.keyword.loganalysisshort}} dall'elenco di servizi disponibili nello spazio. 

    Il valore del campo **name** deve essere utilizzato per modificare il piano. 

    Ad esempio,
	
	```
	$ bx  bx service list
    Invoking 'cf services'...

    Getting services in org MyOrg / space dev as xxx@ibm.com...
    OK

    name                           service                  plan             bound apps            last operation
    Log Analysis-m2                ibmLogAnalysis           premium                                update succeeded
    ```
	{: screen}
    
3. Aggiorna o riduci il tuo piano. Esegui il comando `bx service update`.
    
	```
	bx service update service_name [-p new_plan]
	```
	{: codeblock}
	
	dove 
	
	* *service_name* è il nome del tuo servizio. Per ottenere il valore, puoi eseguire il comando `bx service list`.
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
	    <td>standard</td>
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
	bx service update "Log Analysis-m2" -p standard
    Updating service instance Log Analysis-m2 as xxx@ibm.com...
    OK
	```
	{: screen}

4. Verifica che il nuovo piano è stato modificato. Esegui il comando `bx service list`.

  ```
	bx service list
	```
	{: codeblock}





