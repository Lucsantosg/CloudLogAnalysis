---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Considerações de migração após o upgrade do Elastic Stack para a versão 5.1 
{: #es17_to_es51}

No {{site.data.keyword.Bluemix}}, a pilha ElasticSearch (ELK) é submetida a upgrade da versão 1.7 para a versão 5.1. Novos recursos, novas URLs para alimentar logs e novas URLs para analisar logs no Kibana estão disponíveis. Para obter mais informações, veja [ElasticSearch 5.1 ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

Esse recurso não se aplica a usuários que usam o serviço de criação de log com contêineres do Docker que são implementados em um cluster do Kubernetes. 

## Regiões
{: #regions}

O Elastic versão 5.1 está disponível na região a seguir:

* 
* Sul dos Estados Unidos
* Alemanha
* Sydney


## O que há de novo
{: #features}

1. URLs diferentes para trabalhar com logs e métricas.

    No Elastic 1.7, a mesma URL foi compartilhada para exibir e monitorar logs e métricas. Com o upgrade para o Elastic 5.1, você tem URLs separadas para visualizar logs e métricas. Para obter mais informações, consulte [criação de URLs](#logging).
    
2. Suporte para o Kibana 5,1.

    É possível ativar o Kibana por meio da UI do {{site.data.keyword.Bluemix_notm}} ou diretamente da nova URL de criação de log. Para obter mais informações, veja [Navegando para o painel do Kibana](/docs/services/CloudLogAnalysis/kibana/launch.html#launch).
    
    O Kibana 3 e o Kibana 4 foram descontinuados.
	
	**Nota:** há URLs diferentes por região. O acesso aos painéis do Kibana 4 está atualmente disponível no Reino Unido para você comparar e migrar seus painéis para os do Kibana 5.1. 
    
    Deve-se migrar seus painéis para o ambiente do Elastic 5.1.
    
    Para obter mais informações sobre o Kibana 5.1, veja [Guia do Usuário do Kibana ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
3. Incluído sufixos tipo baseados em campos customizados.

    É possível configurar campos customizados como campos de procura do Kibana. Cada campo que estiver disponível em uma mensagem será analisado para o tipo de campo que corresponder ao seu valor. Por exemplo, cada campo na mensagem JSON a seguir: 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    está disponível como um campo que pode ser usado para filtragem e procuras:

    * field1 é analisado como field1_str do tipo sequência.
    * field2 é analisado como field1_int do tipo número inteiro.
    * field3 é analisado como field3_bool do tipo booleano.
    * field4 é analisado como field4_str do tipo sequência.
    
    A mensagem JSON de amostra é um log que você enviou para o serviço de criação de log. 

    **Nota:** esse recurso está disponível somente no Elastic 5.1. Esse recurso não está disponível no Elastic 1.7 para evitar quebra de painéis do Kibana3.


## URLs de criação de log
{: #logging}

URLs diferentes são usadas para enviar logs para o {{site.data.keyword.Bluemix_notm}} e para analisar dados no Kibana.

A tabela a seguir lista as URLs para a região Sul dos EUA:

<table>
  <caption>Tabela 1. URLs para a região Sul dos EUA</caption>
    <tr>
      <th>Tipo</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>Ingestão URL para logs</td>
    <td>Logs.opvis.bluemix.net:9091</td>
  	<td>Ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL para analisar logs Kibana</td>
    <td>[Https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[Https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

A tabela a seguir lista as URLs para a região Reino Unido:

<table>
  <caption>Tabela 2. URLs para a região Reino Unido</caption>
  <tr>
     <th>Tipo</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>Ingestão URL para logs</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>URL para analisar logs Kibana</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

A tabela a seguir lista as URLs para a região Frankfurt:

<table>
  <caption>Tabela 3. URLs para a região Frankfurt</caption>
  <tr>
     <th>Tipo</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>Ingestão URL para logs</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>URL para analisar logs Kibana</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



