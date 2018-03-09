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


# Vom Standard abweichende Protokolldaten aus einem Container erfassen (veraltet)
{: #logging_containers_other_logs}

Zur Erfassung von Daten aus vom Standard abweichenden Protokollpositionen innerhalb eines Containers, der in der {{site.data.keyword.Bluemix_notm}}-verwalteten Infrastruktur bereitgestellt wird, setzen Sie die Umgebungsvariable auf **LOG_LOCATIONS**, wenn Sie einen Container erstellen. 
{:shortdesc}

* Fügen Sie die Umgebungsvariable **LOG_LOCATIONS** mit einem Pfad zur Protokolldatei hinzu, wenn Sie den Container erstellen. 
* Sie können mehrere Protokolldateien hinzufügen, indem Sie sie durch Kommas getrennt angeben. 

## Vom Standard abweichende Protokolldaten über die IBM Cloud-Konsole erfassen
{: #logging_containers_collect_data_ui}

Führen Sie die folgenden Schritte aus, um vom Standard abweichende Daten über die Konsole zu erfassen:

1. Wählen Sie im Katalog die Option **Container** und dann ein Image aus. 

    Die angezeigte Imageliste enthält Images, die von {{site.data.keyword.IBM_notm}} zur Verfügung gestellt werden, und Images, die in Ihrer privaten {{site.data.keyword.Bluemix_notm}}-Registry gespeichert sind. 

2. Definieren Sie Ihren Container. Wählen Sie den Typ aus, geben Sie einen Namen für den Container ein, wählen Sie die Größe aus und definieren Sie weitere Attributdetails wie IP-Adresse und Ports. Weitere Informationen finden Sie unter [Einzelnen Container über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle erstellen und bereitstellen](/docs/containers/container_single_ui.html#gui). 

3. Erweitern Sie den Abschnitt **Erweiterte Optionen** und wählen Sie die Option **Neue Umgebungsvariable hinzufügen** aus.

4. Fügen Sie die Variable **LOG_LOCATIONS** hinzu und geben Sie als Wert der Variablen das Protokoll an, das Sie analysieren wollen.

    Beispiel: Wenn Sie einen Container hinzufügen, der auf dem aktuellsten Liberty-Image basiert, setzen Sie zum Analysieren der Protokolldatei *dpkg.log* die Umgebungsvariable auf den folgenden Wert:
    
    <table>
      <caption>Tabelle 1. Beispielwert für Protokollpositionen</caption>
      <tbody>
        <tr>
          <th align="center">Variablenname</th>
          <th align="center">Wert</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Klicken Sie auf **Erstellen**.

Das Container-Dashboard wird geöffnet. Überprüfen Sie, ob der Status des Containers mit *Aktiv* angegeben wird. Prüfen Sie anschließend die Protokolle auf der Registerkarte **Überwachung und Protokolle**.


## Vom Standard abweichende Protokolldaten über die Befehlszeilenschnittstelle erfassen
{: #logging_containers_collect_data_cli}

Führen Sie die folgenden Schritte aus, um vom Standard abweichende Protokolldaten über die Befehlszeilenschnittstelle (CLI) zu erfassen:

1. Richten Sie ein Terminal zur Verwendung der {{site.data.keyword.containershort}}-Befehlszeilenschnittstelle ein. Weitere Informationen finden Sie unter [{{site.data.keyword.containershort}}-Benutzerschnittstelle einrichten](/docs/containers/container_cli_cfic_install.html).

2. Melden Sie sich bei der Cloud Foundry-Befehlszeilenschnittstelle mit dem folgenden Befehl an: `bx login`. Geben Sie bei entsprechender Aufforderung Ihre {{site.data.keyword.IBM_notm}}-ID und das zugehörige Kennwort, Ihre Organisation und den Bereich ein. 

3. Melden Sie sich beim {{site.data.keyword.containershort}} mit dem folgenden Befehl an: `bx cf ic login`

4. Erstellen Sie einen einzelnen Container aus einem Image. Schließen Sie die Umgebungsvariable LOG_LOCATIONS ein, um vom Standard abweichende Protokollpositionen anzugeben.  

    Wenn Sie eine angepasste Position hinzufügen wollen, sodass Sie die entsprechenden Protokollinformationen in Kibana anzeigen können, fügen Sie die Umgebungsvariable **LOG_LOCATIONS** hinzu, wenn Sie den Container erstellen. Geben Sie den folgenden Befehl ein:
    
    `docker run -p Portnummer -e "LOG_LOCATIONS=log1,log2" --name Containername registry.Domänenname/Imagename:imageTag`
    
    Dabei gilt:
    
     <table>
      <caption>Tabelle 3. Befehlsoptionen</caption>
      <tbody>
        <tr>
          <th align="center">Option</th>
          <th align="center">Beschreibung</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> Wenn Sie Ihre App über das Internet zugänglich machen wollen, müssen Sie einen öffentlichen Port verfügbar machen. Schließen Sie alle Ports ein, die in der Dockerfile für das Image, das Sie verwenden, angegeben sind. <br> Sie können zwischen UDP und TCP zur Angabe des gewünschten IP-Protokolls wählen. Wenn Sie kein Protokoll angeben, wird Ihr Port automatisch für den TCP-Datenverkehr zugänglich gemacht. <br> Wenn Sie einen öffentlichen Port verfügbar machen, erstellen Sie eine Sicherheitsgruppe für öffentliches Netz (Public Network Security Group) für Ihren Container, die es Ihnen ermöglicht, öffentliche Daten nur über den verfügbar gemachten Port zu senden und zu empfangen. Alle anderen öffentlichen Ports werden geschlossen und können nicht für den Zugriff auf Ihre App über das Internet verwendet werden. <br> Sie können mehrere Ports mit mehreren Optionen -p einschließen. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Legen Sie eine Umgebungsvariable fest. <br> Sie können mehrere Schlüssel separat auflisten. Schließen Sie den Namen der Variablen und den Wert in Anführungszeichen ein. <br> Wenn Sie eine zu überwachende Protokolldatei im Container hinzufügen wollen, schließen Sie die Umgebungsvariable LOG_LOCATIONS mit einem Pfad zu der Protokolldatei ein.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Definiert den Namen des Containers.</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">Die Registry in der öffentlichen Region. Beispiel: Für die Region 'USA (Süden)' ist der Standarddomänenname: `ng.bluemix.net`. Für die Region 'Vereinigtes Königreich' ist der Standarddomänenname: `eu-gb.bluemix.net`. </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">Der Name des Images, das Sie hinzufügen wollen.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">Der Tag des Images, das Sie hinzufügen wollen.</td>
        </tr>
      </tbody>
    </table>
    
    Verwenden Sie zum Beispiel den folgenden Befehl, um einen Container auf der Basis des letzten Liberty-Image zu erstellen und die Protokolldatei `/var/log/dpkg.log` einzuschließen: 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    Die Datei 'dpkg.log' ist eine Ubuntu-Standardprotokolldatei, die normalerweise bei der Erstellung eines Containers generiert wird, jedoch nicht durch eine Push-Operation automatisch an Kibana übertragen wird.

Um den Status des Containers zu überprüfen, führen Sie den Befehl `docker ps` aus. Wenn der Status *aktiv* (Running) ist, prüfen Sie das Protokoll in der {{site.data.keyword.Bluemix_notm}}-Konsole, über die Befehlszeile oder in Kibana.



