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

# Analisando logs na UI do Bluemix
{: #analyzing_logs_bmx_ui}

No {{site.data.keyword.Bluemix}}, é possível visualizar, filtrar e analisar logs por meio da guia de log que está disponível para cada app Cloud Foundry ou contêiner do Docker que é executado na infraestrutura gerenciada pelo {{site.data.keyword.IBM_notm}}.
{:shortdesc}

##  Navegando para os logs de um app Cloud Foundry
{: #launch_logs_tab_bmx_ui_cf}

Para ver os logs de implementação ou de tempo de execução de um app Cloud Foundry, conclua as
etapas a seguir:

1. No painel Apps, clique no nome do seu app Cloud Foundry. 
    
2. Na página de detalhes do app, clique em **Logs**.
    
    Na guia **Logs**, é possível visualizar os logs recentes para seu app ou
acompanhar os logs em tempo real. Além disso, é possível filtrar logs por componente (tipo de log), por ID da instância do app e por erro.
    
Por padrão, os logs que estão disponíveis para análise no
console do {{site.data.keyword.Bluemix_notm}}
incluem dados das últimas 24 horas.

**Dica:** para analisar dados para um período customizado que precede as últimas 24
horas, consulte [Análise de log avançada com
o Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana). 





##  Navegando para os logs de um contêiner do Docker que é gerenciado no Bluemix
{: #launch_logs_tab_bmx_ui_containers}

Para ver os logs de implementação ou tempo de execução de um contêiner do Docker que é implementado na infraestrutura em Nuvem gerenciada pelo {{site.data.keyword.IBM_notm}}, conclua as etapas a seguir:

1. No painel Apps, clique no contêiner único ou no grupo de contêiner. 
    
2. Na página de detalhes do app, clique em **Monitoramento e Logs**.

3. Selecione a guia **Criação de log**.
    
    Na guia **Criação de log**, é possível visualizar os logs recentes para
seu contêiner ou acompanhar os logs em tempo real. 
	
	
	

## Formato de log para logs do app CF
{: #log_format_cf}

Os logs para apps Cloud Foundry do {{site.data.keyword.Bluemix_notm}} são exibidos em um formato
fixo, semelhante ao padrão a seguir:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

Cada entrada de log contém os campos a seguir:

| Campo | Descrição |
|-------|-------------|
| Registro de data e hora | O tempo da instrução de log. O registro de data e hora é definido até o milissegundo. |
| Componente | O componente que produz o log. Para obter a lista dos componentes diferentes, consulte
[Origens para apps CF](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Cada tipo de componente é seguido por uma barra e um dígito que indica a instância do aplicativo. 0 é o dígito alocado para a primeira instância, 1 é o dígito alocado para a segunda e assim por diante. |
| Mensagem | A mensagem que é emitida pelo componente. A mensagem varia, dependendo do contexto. |
{: caption="Tabela 1. Campos de entrada de log do app CF" caption-side="top"}


## Formato de log para logs do contêiner
{: #log_format_containers}

Os logs para contêineres são exibidos em um formato fixo, semelhante ao padrão a seguir:

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

Cada entrada de log contém os campos a seguir:

| Campo | Descrição |
|-------|-------------|
| Data/hora | O tempo da instrução de log. O registro de data e hora é definido como um milissegundo.|
| Machine | O nome do host no qual o contêiner está em execução. |
| Mensagem | A mensagem que é emitida. A mensagem varia, dependendo do contexto. |
{: caption="Tabela 2. Campos de entrada de log do contêiner do Docker" caption-side="top"}

