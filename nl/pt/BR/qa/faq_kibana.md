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


# FAQ do Kibana
{: #faq_kibana}

A seguir estão as respostas para perguntas comuns sobre como usar os recursos de criação de log
do {{site.data.keyword.Bluemix}}. {:shortdesc}

* [O que poderei fazer se eu não conseguir ver
os dados na página Descobrir no Kibana?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_discover_kibana)
* [O que poderei fazer se eu receber uma
exceção de autenticação?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_dashboard_kibana)
* [Como ativar Kibana 3](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana3)
* [Por que eu vejo o símbolo? por campos na página Descobrir do Kibana](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana_question)
* [Recebo um erro 403 quando tento mudar o padrão de índice padrão](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#error_403)

## O que poderei fazer se eu não conseguir ver os dados na página Descobrir no Kibana?
{: #logging_qa_no_data_discover_kibana}

Há diferentes cenários em que você talvez não consiga ver dados no Kibana:

1. Ao ativar o Kibana, talvez você não consiga ver nenhum dado na página Descobrir. Você recebe a
seguinte mensagem: **Nenhum resultado localizado.**. 
2. Talvez você esteja trabalhando na página Descobrir no Kibana. No entanto, após um curto período de tempo, você receberá a mensagem **Nenhum resultado localizado.** ao tentar
executar uma tarefa no Kibana.

Para resolver este problema, execute as etapas a seguir:

1. Verifique o *Selecionador de Tempo* que está configurado na página Descobrir e
aumente o período de tempo. 

    **Nota**: por padrão, no {{site.data.keyword.Bluemix_notm}}, o
*Selecionador de Tempo* é configurado para mostrar dados dos últimos 15 minutos.

    Para obter mais informações sobre como configurar o *Selecionador de Tempo*, consulte
[Configurando um filtro de
tempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
       
2. Clique na lupa que está localizada na barra de procura da página *Descobrir*. Os dados da página são atualizados com base na consulta de procura padrão.

    Como alternativa, é possível configurar um período de *Atualização automática*.

    **Nota**: por padrão, no {{site.data.keyword.Bluemix_notm}}, o
período de *Atualização automática* é configurado como **OFF**.
    
    Para obter mais informações sobre como ativá-lo, consulte
[Atualizando
os dados automaticamente](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_refresh_interval).



## O que poderei fazer se eu receber uma
exceção de autenticação?
{: #logging_qa_no_data_dashboard_kibana}

Quando não for possível ver dados exibidos em suas visualizações em uma página Painel e você receber a
mensagem de erro **Erro: Exceção de autorização.**, verifique suas permissões para ver os dados em
cada visualização.

Considere as informações a seguir:
é possível configurar uma ou mais visualizações em uma página Painel. Quando a página Painel faz uma solicitação para reunir os dados que são exibidos por essas visualizações,
somente uma solicitação é emitida para todas as visualizações. Se você não tiver permissões para ver os dados
em uma das visualizações, a solicitação inteira falhará.

Para resolver este problema, execute as etapas a seguir:

1. Identifique as visualizações para as quais você não tem permissões.

    1. Clique no ícone de *lápis* de uma visualização na página *Painel*. A
visualização se abre na página *Visualizar*. Como alternativa, na página
*Visualizar*, carregue uma visualização. 
    2. Verifique se é possível ver os dados.
    
    Repita estas etapas para cada visualização.

2. Solicite acesso para ver dados nessas visualizações no seu administrador em nuvem.

3. Crie uma nova página Painel que exclua as visualizações para as quais você não tem permissões enquanto
recebe acesso para ver dados nas visualizações que estiverem causando o problema. 

    Se você compartilhar o Painel, não exclua as visualizações, já que isso afetará outros membros da
equipe que usam o mesmo painel.

## Como ativar Kibana 3
{: #logging_qa_kibana3}

**Nota**: o Kibana 3 foi descontinuado.

É possível ativar o Kibana 3 por meio de um navegador.

Conclua a etapa a seguir para ativar o Kibana 3 por meio de um navegador:

1. Abra [https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net) para efetuar login na interface com o usuário do Kibana.
    
2. Selecione a versão do Kibana que deseja usar para analisar seus logs.
    * Selecione a guia **Kibana 4** para trabalhar com o Kibana 4. A página Descobrir se abre. Para obter mais informações, consulte [Analisando logs interativamente no Kibana](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Selecione a guia **Kibana 3** para trabalhar com o Kibana 3. O painel do Kibana padrão é aberto. Para obter informações sobre como usar o Kibana 3 para analisar seus logs, consulte [Analisando logs no Kibana 3 (descontinuado)](docs/monitor_log/kibana3/logging_view_kibana3.html#analyzing_logs_Kibana3). Para obter mais informações sobre como customizar um painel do Kibana 3, veja [esta postagem do blog ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/ "Ícone de link externo"){: new_window}.
     

## Por que eu vejo o símbolo? por campos na página Descobrir do Kibana
{: #logging_qa_kibana_question}

Quando você abre a página Descobrir no Kibana, é possível ver um ponto de interrogação `?` por campos listados na seção de campos disponíveis, em vez do caractere `t`. Quando você recarrega a lista de campos, o tipo de campos é analisado, e o ponto de interrogação `?` é substituído pelo caractere `t`. Para obter mais informações, veja [Recarregando a lista de campos](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_reload_fields).


## Recebo um erro 403 quando tento mudar o padrão de índice padrão
{: #error_403}

O padrão de índice padrão não pode ser mudado. 

Se tentar configurar um padrão de índice diferente como o novo padrão, você receberá o erro a seguir: `Config: Error 403 Forbidden`


