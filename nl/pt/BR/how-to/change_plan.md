---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Mudando o plano
{: #change_plan}

É possível mudar seu plano de serviço do {{site.data.keyword.loganalysisshort}} por meio da UI do {{site.data.keyword.Bluemix_notm}} ou executando o comando `bx cf update-service`. É possível fazer upgrade ou reduzir seu plano a qualquer momento.
{:shortdesc}

## Mudando o plano de serviço por meio da UI
{: #change_plan_ui}

Para mudar seu plano de serviço na UI do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}. 

2. Selecione a região, a organização e o espaço em que o serviço do {{site.data.keyword.loganalysisshort}} está disponível.  

3. Clique na instância de serviço do {{site.data.keyword.loganalysisshort}} no *Painel* do {{site.data.keyword.Bluemix_notm}}. 
    
4. Selecione a guia **Plano** no painel {{site.data.keyword.loganalysisshort}}.

    São exibidas informações sobre o seu plano atual.
	
5. Selecione um novo plano para fazer upgrade ou reduzir o seu plano. 

6. Clique em **Salvar**.




## Mudando o plano de serviço por meio da CLI
{: #change_plan_cli}

Para mudar o seu plano de serviço no Bluemix por meio da CLI, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Execute o comando `bx cf services` para verificar o plano atual e para obter o nome do serviço do {{site.data.keyword.loganalysisshort}} na lista de serviços disponíveis no espaço. 

    O valor do campo **nome** é aquele que deve ser usado para mudar o plano. 

    Por
exemplo,
	
	```
	$ bx cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Faça upgrade ou reduzir seu plano. Execute o comando `bx cf update-service`.
    
	```
	bx cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	em que 
	
	* *service_name* é o nome de seu serviço. É possível executar o comando `bx cf services` para obter o valor.
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
	    <td>Padrão</td>
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
	bx cf update-service "Log Analysis-a4" -p standard
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifique se o novo plano é alterado. Execute o `cf services` comando.

    ```
	bx cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   standard                update succeeded
	```
	{: screen}






