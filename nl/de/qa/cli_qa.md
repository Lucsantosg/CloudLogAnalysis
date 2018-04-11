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


# Antworten auf häufig gestellte Fragen zur Verwendung der IBM Cloud-Befehlszeilenschnittstelle
{: #cli_qa}

Im Folgenden finden Sie Antworten auf häufig gestellte Fragen zur Verwendung der {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle mit dem {{site.data.keyword.loganalysisshort}}-Service. 
{:shortdesc}

* [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)
* [Wie installiere ich die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle](/docs/services/CloudLogAnalysis/qa/cli_qa.html#install_bmx_cli)
* [Wie rufe ich die GUID eines Kontos ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid)
* [Wie rufe ich die GUID einer Organisation ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#org_guid)
* [Wie rufe ich die GUID eines Bereichs ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)

## Wie melde ich mich bei IBM Cloud an?
{: #login}

Führen Sie den folgenden Befehl aus, um sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} anzumelden:

```
bx login -a Endpunkt
```
{: codeblock}
	
Dabei ist *Endpunkt* die URL für die Anmeldung bei {{site.data.keyword.Bluemix_notm}}. Diese URL ist für jede Region anders.
	
<table>
    <caption>Liste der Endpunkte für den Zugriff auf {{site.data.keyword.Bluemix_notm}}</caption>
	<tr>
	  <th>Region</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>Deutschland</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>Sydney</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>USA (Süden)</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
	<tr>
	  <td>Vereinigtes Königreich</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
</table>

Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden:
	
```
bx login -a https://api.ng.bluemix.net
```
{: codeblock}

Gehen Sie gemäß den Anweisungen vor. 

Legen Sie dann die Organisation und den Bereich fest. Führen Sie den folgenden Befehl aus:

```
bx target -o Organisationsname -s Bereichsname
```
{: codeblock}

Dabei gilt:

* 'Organisationsname' ist der Name der Organisation.
* 'Bereichsname' ist der Name des Bereichs.

	
	
## Wie installiere ich die IBM Cloud-Befehlszeilenschnittstelle?
{: #install_bmx_cli}

Siehe [{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen und installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).



## Wie rufe ich die GUID eines Kontos ab?
{: #account_guid}
	
Führen Sie die folgenden Schritte aus, um die GUID eines Kontos abzurufen:
	
1. Melden Sie sich bei einer Region, Organisation und bei einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Führen Sie den Befehl `bx iam accounts` aus, um die GUID eines Kontos abzurufen.

    ```
	bx iam accounts
	```
	{: codeblock} 
	
	Um beispielsweise alle Konten mit den entsprechenden GUIDs für Benutzer xxx@yyy.com abzurufen, führen Sie den folgenden Befehl aus:
	
	```
	bx iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## Wie rufe ich die GUID einer Organisation ab?
{: #org_guid}

Führen Sie die folgenden Schritte aus, um die GUID einer Organisation abzurufen:
	
1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Führen Sie den Befehl 'bx iam org' aus, um die GUID der Organisation abzurufen. 

    ```
    bx iam org NAME --guid
    ```
    {: codeblock}
	
    Dabei ist NAME der Name der {{site.data.keyword.Bluemix_notm}}-Organisation.
		
		
		
## Wie rufe ich die GUID eines Bereichs ab?
{: #space_guid}
	
Führen Sie die folgenden Schritte aus, um die GUID eines Bereichs abzurufen:
	
1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Führen Sie den Befehl 'bx iam space' aus, um die GUID des Bereichs abzurufen. 

    ```
    bx iam space NAME --guid
    ```
    {: codeblock}
	
    Dabei ist NAME der Name eines {{site.data.keyword.Bluemix_notm}}-Bereichs. 
	
    Um beispielsweise die GUID für den Bereich *dev* abzurufen, führen Sie den folgenden Befehl aus:
	
    ```
    bx iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		