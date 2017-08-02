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

# Daten mit dem Multi-Tenant Logstash Forwarder senden
{: #send_data_mt}

Zum Senden von Protokolldaten an den {{site.data.keyword.loganalysisshort}}-Service können Sie einen Multi-Tenant Logstash Forwarder (mt-logstash-forwarder) konfigurieren. {:shortdesc}

Um Protokolldaten an 'Log Collection' zu senden, führen Sie die folgenden Schritte aus:

## Schritt 1: Fordern Sie das Protokollierungstoken an.
{: #get_logging_auth_token}

Zum Senden von Daten an den {{site.data.keyword.loganalysisshort}}-Service benötigen Sie Folgendes:

* Eine {{site.data.keyword.IBM_notm}}ID: Diese ID ist für die Protokollierung in {{site.data.keyword.Bluemix_notm}} erforderlich.
* Einen Bereich in einer {{site.data.keyword.Bluemix_notm}}-Organisation: Dies ist der Bereich, an den Sie Protokolle für die Analyse senden wollen.
* Ein Protokollierungstoken zum Senden von Daten. 

Führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an einer Region, einer Organisation und einem Bereich an. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Führen Sie den Befehl `cf logging auth` aus. 

    ```
    cf logging auth
    ```
    {: codeblock}

    Der Befehl gibt die folgenden Informationen zurück:
    
    * Das Protokollierungstoken.
    * Die Organisations-ID: Dies ist die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, bei der Sie angemeldet sind. 
    * Die Bereichs-ID: Die GUID des Bereichs in der Organisation, bei dem Sie angemeldet sind. 
    
    Beispiel:

    ```
    cf logging auth
    +-----------------+--------------------------------------+
    |      NAME       |                VALUE                 |
    +-----------------+--------------------------------------+
    | Access Token    | $(cf oauth-token|cut -d' ' -f2)      |
    | Logging Token   | oT98_bKsdfTz                         |
    | Organization Id | 98450123-6f1c-9999-96a3-0210fjyuwplt |
    | Space Id        | 93f54jh6-b5f5-46c9-9f0e-kfeutpldnbcf |
    +-----------------+--------------------------------------+
    ```
    {: screen}

Weitere Informationen finden Sie unter [cf logging auth](/docs/services/CloudLogAnalysis/reference/logging_cli.html#auth).


## Schritt 2: Multi-Tenant Logstash Forwarder konfigurieren
{: #configure_mt_logstash_forwarder}

Führen Sie die folgenden Schritte aus, um den Multi-Tenant Logstash Forwarder (mt-logstash-forwarder) in der Umgebung zu konfigurieren, von der aus Sie Protokolle an den {{site.data.keyword.loganalysisshort}}-Service senden wollen:

1.	Melden Sie sich als Rootbenutzer an. 

    ```
    sudo -s
    ```
    {: codeblock}
    
2.	Installieren Sie das NTP-Paket (NTP = Network Time Protocol), um die Protokolle zeitlich zu synchronisieren. 

    Beispiel: Prüfen Sie für ein Ubuntu-System, ob für `timedatectl status` Folgendes angezeigt wird: *Network time on: yes*. Ist dies der Fall, ist Ihr Ubuntu-System bereits so konfiguriert, dass 'ntp' verwendet wird, und Sie können diesen Schritt überspringen.
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    Führen Sie die folgenden Schritte aus, um 'ntp' in einem Ubuntu-System zu installieren:

    1.	Führen Sie den folgenden Befehl aus, um die Pakete zu aktualisieren. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Führen Sie den folgenden Befehl aus, um das ntp-Paket zu installieren. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Führen Sie den folgenden Befehl aus, um das ntpdate-Paket zu installieren. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Führen Sie den folgenden Befehl aus, um den Service zu stoppen. 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Führen Sie den folgenden Befehl aus, um die Systemuhr zu synchronisieren. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        Das Ergebnis bestätigt, dass die Zeit angepasst wurde. Beispiel:
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Führen Sie den folgenden Befehl aus, um 'ntpd' erneut zu starten. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        Das Ergebnis bestätigt, dass der Service gestartet wird.

    7.	Führen Sie den folgenden Befehl aus, um den ntpd-Service für den automatischen Start nach einem Ausfall oder Neustart zu aktivieren. 
    
        ```
        service ntp enable
        ```
        {: codeblock}
        
        Als Ergebnis wird eine Liste der Befehle angezeigt, die zur Verwaltung des ntpd-Service verwendet werden können. Beispiel:
        
        ```
        Usage: /etc/init.d/ntpd {start|stop|status|restart|try-restart|force-reload}
        ```
        {: screen}

3. Fügen Sie das Repository für den {{site.data.keyword.loganalysisshort}}-Service im Paketmanager des Systems hinzu. Führen Sie den folgenden Befehl aus:

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
    {: codeblock}

4. Installieren und konfigurieren Sie den Multi-Tenant Logstash Forwarder (mt-logstash-forwarder), um Protokolle aus Ihrer Umgebung an die 'Log Collection' zu senden. 

    1. Führen Sie den folgenden Befehl aus, um den Multi-Tenant Logstash Forwarder (mt-logstash-forwarder) zu installieren:
    
        ```
        apt-get install mt-logstash-forwarder 
        ```
        {: codeblock}
        
    2. Erstellen Sie die mt-logstash-forwarder-Konfigurationsdatei für Ihre Umgebung. Diese Datei enthält Variablen, die verwendet werden, um Logstash Forwarder so zu konfigurieren, dass der Forwarder an den {{site.data.keyword.loganalysisshort}}-Service verwiesen wird.
    
       Bearbeiten Sie die Datei `/etc/mt-logstash-forwarder/mt-lsf-config.sh`. Sie können zum Beispiel den Editor vi verwenden:
               
       ```
       vi /etc/mt-logstash-forwarder/mt-lsf-config.sh
       ```
       {: codeblock}
        
       Um den Forwarder an den {{site.data.keyword.loganalysisshort}}-Service zu verweisen, fügen Sie die folgenden Variablen in die Datei **mt-lsf-config.sh** ein: 
         
       <table>
          <caption>Tabelle 1. Liste der Variablen, die erforderlich sind, um den Forwarder in einer VM an den {{site.data.keyword.loganalysisshort}}-Service zu verweisen </caption>
          <tr>
            <th>Variablenname</th>
            <th>Beschreibung</th>
          </tr>
          <tr>
            <td>LSF_INSTANCE_ID</td>
            <td>ID für Ihre VM. Beispiel: *MyTestVM*. </td>
          </tr>
          <tr>
            <td>LSF_TARGET</td>
            <td>Ziel-URL. Legen Sie den folgenden Wert fest: **https://ingest.logging.ng.bluemix.net:9091**. </td>
          </tr>
          <tr>
            <td>LSF_TENANT_ID</td>
            <td>ID des Bereichs, für den der {{site.data.keyword.loganalysisshort}}-Service zur Erfassung der Protokolle bereit ist, die Sie an {{site.data.keyword.Bluemix_notm}} senden. <br>Verwenden Sie den Wert, den Sie in Schritt 1 erhalten haben.</td>
          </tr>
          <tr>
            <td>LSF_PASSWORD</td>
            <td>Protokollierungstoken. <br>Verwenden Sie den Wert, den Sie in Schritt 1 erhalten haben.</td>
          </tr>
          <tr>
            <td>LSF_GROUP_ID</td>
            <td>Geben Sie für diesen Wert einen angepassten Tag an, den Sie zum Gruppieren zusammengehöriger Protokolle definieren können.</td>
          </tr>
       </table>
        
       Beispiel: Suchen Sie in der folgenden Beispieldatei nach einem Bereich mit der ID *7d576e3b-170b-4fc2-a6c6-b7166fd57912* in der Region 'Vereinigtes Königreich':
        
       ```
       # more mt-lsf-config.sh
       LSF_INSTANCE_ID="myhelloapp"
       LSF_TARGET="ingest.logging.ng.bluemix.net:9091"
       LSF_TENANT_ID="7d576e3b-170b-4fc2-a6c6-b7166fd57912"
       LSF_PASSWORD="oT98_bKsdfTz"
       LSF_GROUP_ID="Group1"
       ```
       {: screen}
        
    3. Starten Sie den Multi-Tenant Logstash Forwarder (mt-logstash-forwarder). 
    
       ```
       service mt-logstash-forwarder start
       ```
       {: codeblock}
        
       Aktivieren Sie für den Multi-Tenant Logstash Forwarder die Funktionalität zum automatischen Starten nach einem Ausfall oder Neustart. 
        
       ```
       service mt-logstash-forwarder enable
       ```
       {: codeblock}
        
       **Tipp:** Um den Service 'mt-logstash forwarder' erneut zu starten, führen Sie den folgenden Befehl aus:
    
       ```
       service mt-logstash-forwarder restart
       ```
       {: codeblock}
        
        
Standardmäßig beobachtet der Forwarder nur das Syslog. Ihre Protokolle stehen in Kibana für die Analyse zur Verfügung.
        

## Schritt 3: Geben Sie weitere Protokolldateien an.
{: #add_logs}

Standardmäßig wird nur die Datei /var/log/syslog vom Forwarder überwacht. Sie können weitere Konfigurationsdateien zum Verzeichnis `/etc/mt-logstash-forwarder/conf.d/syslog.conf/` hinzufügen, damit der Forwarder auch diese überwachen kann. 

Führen Sie die folgenden Schritte aus, um eine Konfigurationsdatei für eine App hinzuzufügen, die in Ihrer Umgebung ausgeführt wird:

1.	Kopieren Sie die Datei `/etc/mt-logstash-forwarder/conf.d/syslog.conf`. 

    **Tipp:** Bearbeiten Sie die Datei syslog.conf nicht, um Protokolldateien hinzuzufügen.
    
    Beispiel: Führen Sie den folgenden Befehl in einem Ubuntu-System aus:
    
    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
        
2.	Bearbeiten Sie die Datei *myapp.conf* mit einem Texteditor und aktualisieren Sie die Datei, indem Sie die Anwendungsprotokolle einfügen, die Sie überwachen wollen. Geben Sie für jedes App-Protokoll den Protokolltyp an. Löschen Sie alle Beispiele, die nicht verwendet werden.

3.	Starten Sie den Multi-Tenant Logstash Forwarder (mt-logstash-forwarder) erneut. 

     Starten Sie den Service 'mt-logstash-forwarder' erneut. Führen Sie den folgenden Befehl aus:
    
    ```
    service mt-logstash-forwarder restart
    ```
    {: codeblock}

**Beispiel**

Wenn Sie Standardausgabe (stdout) oder Standardfehler (stderr) aus einer Hello-App einbeziehen möchten, leiten Sie 'stdout' oder 'stderr' in eine Protokolldatei um. Erstellen Sie eine Forwarder-Konfigurationsdatei für die App. Starten Sie 'mt-logstash-forwarder' anschließend neu.

1.	Kopieren Sie die Datei `/etc/mt-logstash-forwarder/conf.d/syslog.conf`. 

    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
    
2. Bearbeiten Sie die Konfigurationsdatei *myapp.conf*.

    Um das JSON-Parsing zu aktivieren, stellen Sie 'is_json' in der Konfigurationsdatei auf 'true' ein.
    
    ```
    {
    "files": [
         # weitere Dateikonfigurationen ausgelassen...
            {
            "paths": [ "/var/log/myhelloapp.log" ],
            "fields": { "type": "helloapplog" },
            "is_json": true
            }
         ]
     }
     ```
     {: screen}
