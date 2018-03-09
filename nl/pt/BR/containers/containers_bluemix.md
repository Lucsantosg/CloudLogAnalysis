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


# Criação de log para um contêiner que é gerenciado pelo IBM Cloud (descontinuado)
{: #containers_bluemix}

É possível visualizar, filtrar e analisar logs para contêineres do Docker que são implementados na infraestrutura gerenciada pelo {{site.data.keyword.IBM}}.
{:shortdesc}

Os logs do contêiner são monitorados e encaminhados de fora do contêiner usando crawlers. Os dados são enviados pelos crawlers para um Elasticsearch com diversos locatários no {{site.data.keyword.Bluemix_notm}}.

A figura a seguir mostra uma visualização de alto nível de criação de log para o {{site.data.keyword.containershort}}:

![Visão geral do componente de alto nível para contêineres implementados na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}} ](images/container_bmx.gif "Visão geral do componente de alto nível para contêineres implementados na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}} ")

Por padrão, os logs a seguir são coletados para um contêiner que está implementado na infraestrutura em nuvem gerenciada pelo {{site.data.keyword.Bluemix_notm}}:

<table>
  <caption>Tabela 2. Logs coletados para contêineres implementados na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}}</caption>
  <tbody>
    <tr>
      <th align="center">Log</th>
      <th align="center">Descrição</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> Por padrão, as mensagens do Docker são armazenadas na pasta
/var/log/messages do contêiner. Esse log inclui mensagens do sistema.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Este é o log do Docker. <br> O arquivo de log do Docker não é armazenado como um arquivo dentro do contêiner, mas é coletado de qualquer maneira. Esse arquivo de log é coletado por padrão, pois ele é a convenção do Docker padrão para expor as informações
de stdout (saída padrão) e stderr (erro padrão) para o contêiner. As informações que qualquer processo de contêiner imprime para stdout e stderr são coletadas. 
      </td>
     </tr>
  </tbody>
</table>




## Analisando logs
{: #logging_containers_ov_methods}

Para analisar dados do log do contêiner, use o Kibana para executar tarefas analíticas avançadas. É possível usar o Kibana, uma plataforma de software livre para visualização e análise de dados, para monitorar, procurar, analisar e visualizar seus dados em uma variedade de gráficos, por exemplo, diagramas e tabelas. Para obter mais informações, veja [Analisando logs no Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).


## Coletando logs customizados
{: #collect_custom_logs}

Para coletar logs adicionais, inclua a variável de ambiente **LOG_LOCATIONS**
com um caminho para o arquivo de log ao criar o contêiner. 

É possível incluir múltiplos arquivos de log separando-os com vírgulas. 

Para obter mais informações, consulte
[Coletando dados de log não
padrão de um contêiner](logging_containers_other_logs.html#logging_containers_collect_data).


## Procurando logs
{: #log_search}

Por padrão, é possível usar o Kibana para procurar até 500 MB de logs por dia no {{site.data.keyword.Bluemix_notm}}. 

O serviço {{site.data.keyword.loganalysisshort}} fornece múltiplos planos. Cada plano possui recursos de procura de log diferentes, por exemplo, o plano *Coleção de logs* permite procurar até 1 GB de dados por dia. Para obter mais informações sobre os planos, veja [Planos de serviços](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## Enviando logs para que seja possível usar os campos em uma mensagem como campos de procura do Kibana
{: #send_data_in_json}

Por padrão, a criação de log é ativada automaticamente para os contêineres. Cada entrada no arquivo de log do Docker é exibida no Kibana no campo `message`. Se você precisar filtrar e analisar seus dados no Kibana usando um campo específico que faça parte da entrada de log do contêiner, configure seu aplicativo para enviar uma saída formatada em JSON válida.

Conclua as etapas a seguir para enviar logs em que as entradas de log do contêiner são analisadas em campos individuais:

1. Efetue a mensagem para um arquivo. 
2. Inclua o arquivo de log na lista de logs não padrão que estão disponíveis para análise de um contêiner. Para obter mais informações, consulte
[Coletando dados de log não
padrão de um contêiner](logging_containers_other_logs.html#logging_containers_collect_data). 
    
Quando as entradas de log JSON são enviadas para o arquivo de log do Docker de um contêiner como STDOUT, elas não são analisadas como JSON. 
    
Se você registra a mensagem em um arquivo e uma mensagem é determinada como JSON válido, os campos são analisados e novos campos são criados para cada campo na mensagem. Somente valores de campos do tipo sequência estão disponíveis para filtragem e classificação no Kibana

## Armazenando logs em Coleção de logs
{: #store_logs}

Por padrão, o {{site.data.keyword.Bluemix_notm}} armazena dados do log por até 3 dias:   

* Um máximo de 500 MB por espaço de dados é armazenado por dia. Qualquer log além desse valor máximo de 500 MB é descartado. As dotações de limite são reconfiguradas diariamente às 0h30 UTC.
* Até 1,5 GB de dados podem ser procurados por um máximo de 3 dias. Os dados do log são substituídos (Primeiro a entrar, Primeiro a sair) depois de atingir 1,5 GB de dados ou depois de 3 dias.

O serviço {{site.data.keyword.loganalysisshort}} fornece planos adicionais que permitem armazenar logs na Coleção de logs o tempo que for necessário. Para obter mais informações sobre o preço de cada plano, veja [Planos de serviços](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

Se você precisar armazenar logs ou procurar logs maiores, será possível provisionar o serviço {{site.data.keyword.loganalysisshort}} e escolher um plano de serviço diferente. Os planos adicionais permitem armazenar logs na Coleção de logs o tempo que for requerido e procurar tamanhos de logs maiores. Para obter mais informações, veja [Planos de serviço](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## Visualizando logs
{: #logging_containers_ov_methods_view_bmx}

É possível visualizar os logs mais recentes de um contêiner que está implementado na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}} usando um dos métodos a seguir:

* Visualize os logs pela UI do {{site.data.keyword.Bluemix_notm}} para monitorar a atividade mais recente do contêiner.
    
    É possível visualizar, filtrar e analisar logs por
meio da guia **Monitoramento e logs** que está disponível para cada contêiner. 
	
	Para ver os logs de implementação ou de tempo de execução de um contêiner do Docker que está implementado na infraestrutura gerenciada pelo {{site.data.keyword.IBM_notm}}, conclua as etapas a seguir:

    1. No painel Apps, clique no contêiner único ou no grupo de contêiner. 
    
    2. Na página de detalhes do app, clique em **Monitoramento e Logs**.

    3. Selecione a guia **Criação de log**. Na guia **Criação de log**, é possível visualizar os logs recentes para
seu contêiner ou acompanhar os logs em tempo real. 
	
* Visualize logs usando a CLI do {{site.data.keyword.containershort}}. Use comandos para gerenciar os logs programaticamente.
    
    É possível visualizar, filtrar e analisar logs por meio da interface da linha de comandos usando o
comando **cf ic logs**. 
	
	Use o comando `bx cf ic logs` para exibir logs de um contêiner no {{site.data.keyword.Bluemix_notm}}. Por exemplo, é possível usar os logs para analisar por que um
contêiner parou ou para revisar a saída do contêiner. 
	
	Para ver os erros do aplicativo para o app que é executado em um contêiner por meio do
comando `cf ic logs`, o aplicativo deve gravar seus logs nos fluxos de saída padrão (STDOUT)
e de saída de erro (STDERR). Se você projetar seu aplicativo para gravar nesses fluxos de saída padrão, será
possível visualizar os logs por meio da linha de comandos, mesmo se o contêiner for encerrado ou travar.

    Para obter mais informações sobre o comando `cf ic logs`, consulte o comando
[cf ic logs](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).



