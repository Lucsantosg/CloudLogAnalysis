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


# Alterando o plano
{: #change_plan}

É possível mudar o seu plano de serviços {{site.data.keyword.loganalysisshort}} em {{site.data.keyword.Bluemix_notm}} no Painel de serviços ou executando o comando `cf update-service`. É possível fazer upgrade ou reduzir seu plano a qualquer momento.
{:shortdesc}

## Mudando o plano de serviço por meio da UI
{: #change_plan_ui}

Para mudar o seu plano de serviço no {{site.data.keyword.Bluemix_notm}} no Painel de serviço, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no serviço {{site.data.keyword.loganalysisshort}} por meio do painel do {{site.data.keyword.Bluemix_notm}}. 
    
2. Selecione a guia **Plano** na UI do {{site.data.keyword.Bluemix_notm}}.

    São exibidas informações sobre o seu plano atual.
	
3. Selecione um novo plano para fazer upgrade ou reduzir o seu plano. 

4. Clique em **Salvar**.



## Mudando o plano de serviço por meio da CLI
{: #change_plan_cli}

Para mudar o seu plano de serviço no Bluemix por meio da CLI, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
	
2. Execute o comando `cf services` para verificar o seu plano atual e para obter o nome do serviço {{site.data.keyword.loganalysisshort}} na lista de serviços que está disponível no espaço. 

    O valor do campo **nome** é aquele que deve ser usado para mudar o plano. 

    Por
exemplo,
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Faça upgrade ou reduzir seu plano. Execute o `cf update-service` comando.
    
	```
	Cf update-service service_name [-p new_plan ]
	```
	{: codeblock}
	
	em que 
	
	* *service_name* é o nome de seu serviço. É possível executar o comando `cf services` para obter o valor.
	* *new_plan* é o nome do plano.
	
	A tabela a seguir lista os diferentes planos e seus valores suportados:
	
	<table>
	  <caption>Tabela 1.  Lista de planos.</caption>
	  <tr>
	    <th>Planejar</th>
	    <th>Nome</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>Lite</td>
	  </tr>
	  <tr>
	    <td>Coleta de Log</td>
	    <td>Premium</td>
	  </tr>
	  <tr>
	    <td>Coleção de logs com procura de 2 GB/dia</td>
	    <td>Premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>Coleção de logs com procura de 5 GB/dia</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>Coleção de logs com procura de 10 GB/dia</td>
	    <td>Premiumsearch10</td>
	  </tr>
	</table>
	
	Por exemplo, para reduzir o seu plano para o plano *Lite*, execute o comando a seguir:
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifique se o novo plano é alterado. Execute o `cf services` comando.

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{






