---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Navegando para o painel do Kibana
{: #launch}

É possível ativar o Kibana do serviço {{site.data.keyword.loganalysisshort}} por meio da UI do {{site.data.keyword.Bluemix}} ou diretamente de um navegador da web.
{:shortdesc}

Para apps CF e contêineres do Docker implementados em uma infraestrutura em nuvem gerenciada pelo {{site.data.keyword.Bluemix_notm}}, é possível ativar o Kibana por meio do {{site.data.keyword.Bluemix_notm}} para visualizar e analisar dados no contexto para o recurso do qual o Kibana é ativado. Por exemplo, é possível ativar seus logs específicos do app CF no Kibana dentro do contexto para esse App específico.
    
Para qualquer recurso em nuvem, como um contêiner do Docker que é implementado em uma infraestrutura do Kubernetes, é possível ativar o Kibana de um link direto do navegador ou do painel do serviço {{site.data.keyword.loganalysisshort}} para ver dados de log agregados de serviços em um espaço fornecido do {{site.data.keyword.Bluemix_notm}}. A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para um espaço na organização do
    {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana
    exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado. 

A tabela a seguir lista alguns recursos em nuvem e os métodos de navegação suportados para ativar o Kibana:

<table>
<caption>Tabela 1. Lista de recursos e métodos de navegação suportados. </caption>
  <tr>
    <th>Recursos</th>
	<th>Navegando para o painel do Kibana por meio do painel do serviço {{site.data.keyword.loganalysisshort}}</th>
    <th>Navegando para o painel do Kibana por meio do painel do Bluemix</th>
    <th>Navegando para o painel do Kibana por meio de um navegador da web</th>
  </tr>
  <tr>
    <td>Aplicativo CF</td>
	<td>Sim</td>
    <td>Sim</td>
    <td>Sim</td>
  </tr>  
  <tr>
    <td>Contêiner implementado em um cluster Kubernetes</td>
	<td>Sim</td>
    <td>Não</td>
    <td>Sim</td>
  </tr>  
  <tr>
    <td>Contêiner implementado em uma infraestrutura em Nuvem gerenciada pelo {{site.data.keyword.Bluemix_notm}}</td>
	<td>Sim</td>
    <td>Sim</td>
    <td>Sim</td>
  </tr>  
</table>

Para obter mais informações sobre Kibana, veja o [Guia do Usuário do Kibana ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Ícone de link externo"){: new_window}.
    

##  Navegando para o Kibana por meio do painel do serviço Log Analysis
{: #launch_Kibana_from_log_analysis}

A consulta usada para filtrar os dados exibidos em Kibana recupera as entradas de log para esse espaço na organização do {{site.data.keyword.Bluemix_notm}}. 
	
As informações de log que o Kibana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Kibana por meio do painel do serviço {{site.data.keyword.loganalysisshort}}:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no serviço {{site.data.keyword.loganalysisshort}} por meio do painel do {{site.data.keyword.Bluemix_notm}}. 
    
2. Selecione a guia **Gerenciado** na UI do {{site.data.keyword.Bluemix_notm}}.

3. Clique em **ATIVAR**. O painel Kibana é aberto.

Por padrão, a página **Descobrir** é carregada com o padrão de índice padrão selecionado e um filtro de tempo configurado para os últimos 15 minutos. 

Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](filter_logs.html#set_time_filter).

	
	
##  Navegando para o Kibana por meio de um navegador da web
{: #launch_Kibana_from_browser}

A consulta usada para filtrar os dados exibidos em Kibana recupera as entradas de log para esse espaço na organização do {{site.data.keyword.Bluemix_notm}}. 
	
As informações de log que o Kibana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Kibana em um navegador:

1. Abra um navegador da web e ative o Kibana. Em seguida, efetue login na interface com o usuário do Kibana.
    
    Por exemplo, a tabela a seguir lista a URL que deve ser usada para ativar o Kibana na região sul dos EUA:
      
    <table>
          <caption>Tabela 1. URLs para ativar o Kibana por região</caption>
           <tr>
            <th>Region</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>Sul dos Estados Unidos</td>
            <td>Https://logging.ng.bluemix.net/ </td>
          </tr>
    </table>
	
	A página Descobrir no Kibana é aberto.
	
2. Selecione o padrão de índice para o espaço do {{site.data.keyword.Bluemix_notm}} do qual você deseja visualizar e analisar dados do log.

    1. Clique em **default-index**.
	
	2. Selecione o padrão de índice do espaço. O formato do padrão de índice é o seguinte:
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    em que *Space_ID* é o GUID do espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja visualizar e analisar dados do log. 
	
Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


	
##  Navegando para o Kibana por meio do painel de um app CF
{: #launch_Kibana_from_cf_app}

A consulta usada para filtrar os dados exibidos no Kibana recupera entradas de log para o app CF do {{site.data.keyword.Bluemix_notm}} do qual o Kibana é ativado.

Para ver os logs de um aplicativo Cloud Foundry no Kibana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no nome ou no contêiner do app no painel do {{site.data.keyword.Bluemix_notm}}. 
    
2. Abra a guia de log na IU do {{site.data.keyword.Bluemix_notm}}.

    Para apps CF, clique em **Logs** na barra de navegação. 
    A guia de logs é aberta.  

3. Clique em **Visualização avançada**. O painel Kibana é aberto.

    Por padrão, a página **Descobrir** é carregada com o modelo de índice padrão selecionado e com um filtro de tempo configurado para os últimos 30 segundos. A consulta de procura é configurada para corresponder todas as entradas do app CF.

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


##  Navegando para o Kibana por meio do painel de um contêiner
{: #launch_Kibana_for_containers}

Esse método se aplica apenas aos contêineres implementados na infraestrutura em nuvem gerenciada pelo {{site.data.keyword.Bluemix_notm}}.

A consulta usada para filtrar os dados exibidos no Kibana recupera entradas de log para o contêiner de onde o Kibana é ativado.

Para ver os logs de um contêiner do Docker no Kibana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no contêiner por meio do painel do {{site.data.keyword.Bluemix_notm}}. 
    
2. Abra a guia de log na IU do {{site.data.keyword.Bluemix_notm}}.

    Para contêineres implementados na infraestrutura em nuvem gerenciada pela {{site.data.keyword.IBM_notm}}, selecione **Monitoramento e logs** na barra de navegação e, em seguida, clique na guia **Criação de log**. 
    
    A guia de logs é aberta.  

3. Clique em **Visualização avançada**. O painel Kibana é aberto.

    Por padrão, a página **Descobrir** é carregada com o modelo de índice padrão selecionado e com um filtro de tempo configurado para os últimos 30 segundos. A consulta de procura é configurada para corresponder todas as entradas do contêiner do Docker.

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).

	



