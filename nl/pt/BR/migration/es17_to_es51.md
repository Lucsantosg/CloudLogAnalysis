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

# Considerações de migração após o upgrade do ELK Stack para a versão 5.1 
{: #es17_to_es51}

No {{site.data.keyword.Bluemix}}, a pilha ElasticSearch (ELK) é submetida a upgrade da versão 1.7 para a versão 2.3. Novos recursos, URLs para alimentar logs e novas URLs para analisar logs no Kibana estão disponíveis. Para obter mais informações, veja [ElasticSearch 5.1 ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "Ícone de link externo").
{:shortdesc}

Esse recurso não se aplica a usuários que usam o serviço de criação de log com contêineres do Docker que são implementados em um cluster do Kubernetes. Esses contêineres já usam a pilha ELK versão 2.3.

## Regiões
{: #regions}

A pilha ELK versão 5.1 está disponível na região a seguir:

* Sul dos Estados Unidos


## O que há de novo
{: #features}

1. URLs diferentes para trabalhar com logs e métricas.

    No ELK 1.7, a mesma URL é compartilhada para exibir e monitorar logs e métricas. Com o upgrade para o ELK 5.1, você tem URLs separadas para visualizar logs e métricas. Para obter mais informações, consulte [criação de URLs](#logging).
    
2. Suporte para o Kibana 5,1. 

    É possível ativar o Kibana por meio da UI do {{site.data.keyword.Bluemix_notm}} ou diretamente da nova URL de criação de log. Para obter mais informações, veja [Analisando logs com o Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
    
    O Kibana 3 foi descontinuado. É possível ativar o Kibana 3 por meio da [URL de criação de log do ELK 1.7](#logging). Há URLs diferentes por região. **Nota:** o acesso aos painéis do Kibana 3 está atualmente disponível para você comparar e migrar os painéis do Kibana 3 para aqueles do Kibana 5.1. 
    
    Se você tiver painéis do Kibana construídos na pilha ELK 1.7, eles deverão ser migrados para o ambiente do ELK 5.1.
    
    Para obter mais informações sobre o Kibana 5.1, veja [Guia do Usuário do Kibana ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Ícone de link externo"){: new_window}.
    
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


## Registro 
{: #logging}

São usadas URLs diferentes para enviar logs para o {{site.data.keyword.Bluemix_notm}} e para analisar dados no Kibana.

A tabela a seguir lista a nova URL da região sul dos EUA:

<table>
  <caption>URLs para a região sul dos EUA</caption>
    <tr>
      <th>Tipo</th>
      <th>ELK 1,7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>Ingestão URL para logs</td>
    <td>Logs.opvis.bluemix.net:9091</td>
	<td>Ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL para analisar logs Kibana</td>
    <td>Https://logmet.ng.bluemix.net</td>
	<td>Https://logging.ng.bluemix.net</td>
  </tr>
</table>

