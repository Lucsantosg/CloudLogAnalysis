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


# Berechtigungen erteilen
{: #grant_permissions}

In {{site.data.keyword.Bluemix}} können Sie Benutzern eine oder mehrere Rollen zuweisen. Diese Rollen definieren, welche Tasks für diesen Benutzer für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service aktiviert sind. 
{:shortdesc}



## Einem Benutzer über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle eine IAM-Richtlinie zuweisen
{: #grant_permissions_ui_account}

Um einem Benutzer Berechtigungen für das Anzeigen und Verwalten von Kontoprotokollen zu erteilen, müssen Sie für diesen Benutzer eine Richtlinie hinzufügen, die die Aktionen beschreibt, die der Benutzer im Rahmen des {{site.data.keyword.loganalysisshort}}-Service im Konto durchführen kann. Nur Kontoeigner können Benutzern einzelne Richtlinien zuweisen.

Führen Sie in {{site.data.keyword.Bluemix_notm}} die folgenden Schritte aus, um einem Benutzer Berechtigungen für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten > Konto > Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste mit Benutzern und den entsprechenden E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer ein Mitglied des Kontos ist, wählen Sie den Benutzernamen aus der Liste aus oder klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie unter [Benutzer einladen](/docs/iam/iamuserinv.html#iamuserinv) Informationen zum entsprechenden Vorgehen in diesem Fall.

4. Klicken Sie im Abschnitt **Zugriffsrichtlinien** auf **Servicerichtlinien zuweisen** und wählen Sie anschließend **Zugriff auf Ressourcen zuweisen**.

    Das Fenster *Ressourcenzugriff an Benutzer zuweisen** wird geöffnet.

5. Geben Sie Informationen zu der Richtlinie ein. In der folgenden Tabelle sind die Felder aufgeführt, die zum Definieren einer Richtlinie erforderlich sind: 

    <table>
	  <caption>Liste von Feldern für die Konfiguration einer IAM-Richtlinie.</caption>
	  <tr>
	    <th>Feld</th>
		<th>Wert</th>
	  </tr>
	  <tr>
	    <td>Services</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>Regionen</td>
		<td>Sie können die Regionen angeben, für die der Benutzer Zugriff für die Arbeit mit Protokollen erhält. Wählen Sie nacheinander eine oder mehrere Regionen aus oder wählen Sie **Alle aktuellen Regionen** aus, um Zugriff auf alle Regionen zu erteilen.</td>
	  </tr>
	  <tr>
	    <td>Serviceinstanz</td>
		<td>Wählen Sie *Alle Serviceinstanzen* aus.</td>
	  </tr>
	  <tr>
	    <td>Rollen</td>
		<td>Wählen Sie eine oder mehrere IAM-Rollen aus. <br>Gültige Rollen sind: *Administrator*, *Operator*, *Editor* und *Anzeigeberechtigter*. <br>Weitere Informationen zu den Aktionen, die pro Rolle zulässig sind, finden Sie unter [IAM-Rollen](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).
		</td>
	  </tr>
     </table>
	
6. Klicken Sie auf **Richtlinie zuweisen**.
	
Die von Ihnen konfigurierte Richtlinie gilt für die ausgewählten Regionen. 

## Einem Benutzer über die Befehlszeile eine IAM-Richtlinie zuweisen
{: #grant_permissions_commandline}

Um einem Benutzer Berechtigungen für das Anzeigen und Verwalten von Kontoprotokollen zu erteilen, müssen Sie dem Benutzer eine IAM-Rolle zuordnen. Weitere Informationen zu IAM-Rollen und den jeweils dafür aktivierten Tasks für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service finden Sie unter [IAM-Rollen](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).

Diese Operation kann nur vom Kontoeigner durchgeführt werden.

Führen Sie die folgenden Schritte aus, um einem Benutzer über die Befehlszeile Zugriff zum Anzeigen von Kontoprotokollen zu erteilen:

1. Rufen Sie die Konto-ID ab. 

    Führen Sie den folgenden Befehl aus, um die Konto-ID abzurufen:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Es wird eine Liste von Konten mit den jeweiligen GUIDs angezeigt.
	
	Exportieren Sie die Konto-ID des Kontos, für das einem Benutzer Berechtigungen erteilt werden sollen, beispielsweise in eine Shellvariable wie '$acct_id':
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. Rufen Sie die {{site.data.keyword.Bluemix_notm}}-ID des Benutzers ab, dem Berechtigungen erteilt werden sollen.

    1. Zeigen Sie die Benutzer an, die dem Konto zugeordnet sind. Führen Sie dazu den folgenden Befehl aus:
	
	    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. Rufen Sie die GUID des Benutzers ab. **Hinweis:** Dieser Schritt muss von dem Benutzer ausgeführt werden, dem Berechtigungen erteilt werden sollen.
	
	    Fordern Sie den Benutzer beispielsweise zum Ausführen der folgenden Befehle aus, um seine Benutzer-ID abzurufen:
		
		Rufen Sie das IAM-Token ab. Weitere Informationen finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle abrufen](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

        Rufen Sie die Daten aus dem IAM-Token ab, die sich zwischen den ersten beiden Punkten in dem Token befinden. Exportieren Sie die Daten in eine Shellvariable '$user_data'. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Führen Sie zum Abrufen der Benutzer-ID beispielsweise den folgenden Befehl aus. Dieser Befehl verwendet 'jq' in diesem Beispiel, um die Informationen in mit JSON formatierten Text zu entschlüsseln:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		Die Ausgabe nach dem Ausführen des Befehls sieht folgendermaßen aus:
		
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
		
		Senden Sie die Benutzer ID an den Kontoeigner.
		
	3. Exportieren Sie die Benutzer-ID in eine Shellvariable wie `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Wenn der Benutzer nicht bereits Mitglied in dem Konto ist, laden Sie ihn ein. Weitere Informationen hierzu finden Sie unter [Benutzer einladen](/docs/iam/iamuserinv.html#iamuserinv).

    Führen Sie beispielsweise den folgenden Befehl aus, um den Benutzer 'xxx@yyy.com' zur Teilnahme am Konto 'zzz@ggg.com' einzuladen:
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Erstellen Sie einen Richtliniendateiname. 

    Verwenden Sie beispielsweise die folgende Vorlage, um Berechtigungen in der Region 'USA (Süden)' zu gewähren:
	
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
	
	Geben Sie der Richtliniendatei einen Namen: `policy.json`
	
5. Rufen Sie das IAM-Token für Ihre Benutzer-ID ab.

    Weitere Informationen finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle abrufen](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

    Exportieren Sie das IAM-Token in eine Shellvariable wie `$iam_token`:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Erteilen Sie dem Benutzer Berechtigungen für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service. 

   Führen Sie den folgenden cURL-Befehl aus, um Berechtigungen in der Region 'USA (Süden)' zu erteilen:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Führen Sie den folgenden cURL-Befehl aus, um Berechtigungen in der Region 'Vereinigtes Königreich' zu erteilen:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
Nachdem Sie einem Benutzer Berechtigungen erteilt haben, kann sich dieser Benutzer bei {{site.data.keyword.Bluemix_notm}} anmelden und die Kontoprotokolle anzeigen.



## Benutzerberechtigungen zum Anzeigen von Bereichsprotokollen über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle erteilen
{: #grant_permissions_ui_space}

Um Benutzerberechtigungen zum Anzeigen von Protokollen in einem Bereich zu erteilen, müssen Sie de Benutzer eine Cloud Foundry-Rolle zuweisen, die die Aktionen beschreibt, die dieser Benutzer im Rahmen des {{site.data.keyword.loganalysisshort}}-Service im Bereich ausführen kann. 

Führen Sie die folgenden Schritte aus, um einem Benutzer Berechtigungen für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten > Konto > Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste mit Benutzern und den entsprechenden E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer ein Mitglied des Kontos ist, wählen Sie den Benutzernamen aus der Liste aus oder klicken Sie im Menü **Aktionen** auf *Benutzer verwalten*.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie unter [Benutzer einladen](/docs/iam/iamuserinv.html#iamuserinv) Informationen zum entsprechenden Vorgehen in diesem Fall.

4. Wählen Sie **Cloud Foundry-Zugriff** und anschließend die Organisation aus.

    Die in dieser Organisation verfügbaren Bereiche werden aufgelistet.

5. Wählen Sie nur einen Bereich aus. Anschließend wählen Sie aus der Menüaktion **Bereichsrolle bearbeiten** aus.

6. Wählen Sie mindestens eine Bereichsrolle aus. Gültige Rollen sind: *Manager*, *Entwickler* und *Prüfer*
	
7. Klicken Sie auf **Rolle speichern**.




