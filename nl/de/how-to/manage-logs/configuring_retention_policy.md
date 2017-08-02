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

# Protokollaufbewahrungsrichtlinie konfigurieren
{: #configuring_retention_policy}

Mit dem Befehl **cf logging option** wird die Aufbewahrungsrichtlinie angezeigt und konfiguriert, die die Dauer (in Tagen) angibt, für die die Protokolle in 'Log Collection' aufbewahrt werden. Standardmäßig werden Protokolle 30 Tage lang aufbewahrt. Wenn der Aufbewahrungszeitraum abgelaufen ist, werden die Protokolle automatisch gelöscht. Standardmäßig ist die Aufbewahrungsrichtlinie inaktiviert.
{:shortdesc}

In einem Konto können verschiedene Aufbewahrungsrichtlinien definiert sein. Sie können eine globale Kontenrichtlinie und einzelne Bereichsrichtlinien haben. Die Aufbewahrungsrichtlinie, die Sie auf Kontoebene festlegen, legt die maximale Anzahl von Tagen fest, für die Protokolle aufbewahrt werden. Wenn Sie eine Bereichsaufbewahrungsrichtlinie für einen bestimmten Zeitraum festlegen, der länger als der Zeitraum auf Kontoebene ist, wird die Richtlinie angewendet, die Sie als letzte für diesen Bereich konfiguriert haben. 


## Protokollaufbewahrungsrichtlinie für einen Bereich inaktivieren
{: #disable_retention_policy_space}

Führen Sie die folgenden Schritte aus, um eine Aufbewahrungsrichtlinie zu inaktivieren:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, für die/den Sie eine Protokollaufbewahrungsrichtlinie festlegen wollen. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Legen Sie den Aufbewahrungszeitraum auf **-1** fest, um den Aufbewahrungszeitraum zu inaktivieren. Führen Sie den folgenden Befehl aus:

    ```
    cf logging option -r -1
    ```
    {: codeblock}
    
**Beispiel**
    
Um beispielsweise den Aufbewahrungszeitraum für einen Bereich mit der ID *d35da1e3-b345-475f-8502-cfgh436902a3* zu inaktivieren, führen Sie den folgenden Befehl aus:

```
cf logging option -r -1
```
{: codeblock}

Die Ausgabe sieht wie folgt aus:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen} 



## Protokollaufbewahrungsrichtlinie für einen Bereich überprüfen
{: #check_retention_policy_space}

Um die Aufbewahrungsdauer abzurufen, die für einen {{site.data.keyword.Bluemix_notm}}-Bereich festgelegt ist, führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, für die/den Sie eine Protokollaufbewahrungsrichtlinie festlegen wollen. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Rufen Sie den Aufbewahrungszeitraum ab. Führen Sie den folgenden Befehl aus:

    ```
    cf logging option
    ```
    {: codeblock}

    Die Ausgabe sieht wie folgt aus:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Protokollaufbewahrungsrichtlinie für alle Bereiche in einem Konto überprüfen
{: #check_retention_policy_account}

Um die Aufbewahrungsdauer abzurufen, die für jeden {{site.data.keyword.Bluemix_notm}}-Bereich in einem Konto festgelegt ist, führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, für die/den Sie eine Protokollaufbewahrungsrichtlinie festlegen wollen. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Rufen Sie den Aufbewahrungszeitraum für jeden Bereich in dem Konto ab. Führen Sie den folgenden Befehl aus:

    ```
    cf logging option -a
    ```
    {: codeblock}

    Die Ausgabe sieht wie folgt aus:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    | fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Protokollaufbewahrungsrichtlinie auf Kontoebene festlegen
{: #set_retention_policy_space}

Um die Aufbewahrungsdauer für ein {{site.data.keyword.Bluemix_notm}}-Konto anzuzeigen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, für die/den Sie eine Protokollaufbewahrungsrichtlinie festlegen wollen. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Legen Sie den Aufbewahrungszeitraum fest. Führen Sie den folgenden Befehl aus:

    ```
    cf logging option -r *Anzahl_von_Tagen* - a
    ```
    {: codeblock}
    
    Dabei ist *Anzahl_von_Tagen* eine ganze Zahl, die die Aufbewahrungsdauer von Protokollen in Tagen angibt. 
    
    
**Beispiel**
    
Beispiel: Wenn alle Protokolltypen nur für 15 Tage in Ihrem Konto verbleiben sollen, führen Sie den folgenden Befehl aus:

```
cf logging option -r 15 -a
```
{: codeblock}

Die Ausgabe enthält einen Eintrag für jeden Bereich des Kontos, einschließlich Informationen zum Aufbewahrungszeitraum:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        15 |
+--------------------------------------+-----------+
| fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
+--------------------------------------+-----------+
```
{: screen}

## Protokollaufbewahrungsrichtlinie für einen Bereich festlegen
{: #set_retention_policy_account}

Um die Aufbewahrungsdauer für einen {{site.data.keyword.Bluemix_notm}}-Bereich anzuzeigen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, für die/den Sie eine Protokollaufbewahrungsrichtlinie festlegen wollen. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Legen Sie den Aufbewahrungszeitraum fest. Führen Sie den folgenden Befehl aus:

    ```
    cf logging option -r *Anzahl_von_Tagen*
    ```
    {: codeblock}
    
    Dabei ist *Anzahl_von_Tagen* eine ganze Zahl, die die Aufbewahrungsdauer von Protokollen in Tagen angibt.
    
    
**Beispiel**
    
Beispiel: Wenn Protokolle für ein ganzes Jahr in einem Bereich verbleiben sollen, führen Sie den folgenden Befehl aus:

```
cf logging option -r 365
```
{: codeblock}

Die Ausgabe sieht wie folgt aus:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |       365 |
+--------------------------------------+-----------+
```
{: screen}


