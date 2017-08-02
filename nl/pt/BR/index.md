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

# Tutorial Introdução
{: #getting-started-with-cla}

Neste tutorial de introdução, forneceremos orientação durante as etapas para executar tarefas analíticas avançadas usando o serviço {{site.data.keyword.loganalysislong}}. Aprenda a procurar e analisar logs do contêiner para um app que é implementado em um cluster do Kubernetes.
{:shortdesc}

## Antes de iniciar
{: #prereqs}

Crie um [{{site.data.keyword.Bluemix_notm}} conta](https://console.bluemix.net/registration/). Seu ID do usuário deve ser um membro ou um proprietário de uma conta do {{site.data.keyword.Bluemix_notm}} com permissões para criar clusters do Kubernetes, implementar apps nos clusters e consultar os logs no {{site.data.keyword.Bluemix_notm}} para análise avançada no Kibana.

Abra uma sessão de terminal na qual você possa gerenciar o cluster do Kubernetes e implementar apps por meio da linha de comandos. Os exemplos neste tutorial são fornecidos para um sistema Ubuntu Linux.

[Instale os plug-ins da CLI](/docs/containers/cs_cli_install.html#cs_cli_install_steps) em seu ambiente local para gerenciar o serviço {{site.data.keyword.containershort}} por meio da linha de comandos. 



## Etapa 1: implementar um app em um cluster do Kubernetes
{: #step1}

1. [Criar um Kubernetes cluster](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. [Configure o contexto do cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) em um terminal Linux. Após o contexto ser configurado, é possível gerenciar o cluster do Kubernetes e implementar o aplicativo no cluster do Kubernetes.

3. Implemente e execute um aplicativo de amostra no cluster do Kubernetes. [Conclua as etapas para a lição 1](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

    O app é Hello World Node.js:

    ```
    var express = require('express')
var app = express()

    app.get('/', function(req, res) {
      Res.send (' Hello world! Your app is up and running in a cluster!\n')
    })
    App.listen (8080, function () {
      console.log('Sample app is listening on port 8080.')
    })
    ```
	{: codeblock}

    Quando o app é implementado, a coleção de logs é ativada automaticamente para quaisquer entradas de log que são enviadas pelo app para stdout (saída padrão) e stderr (erro padrão). 

    Nesse app de amostra, quando você testar o app em um navegador, ele gravará a mensagem a seguir no stdout: `Sample app is listening on port 8080.`

## Etapa 2: navegar para o painel do Kibana
{: #step2}

Para analisar dados do log para um cluster, deve-se acessar o Kibana na região Pública de nuvem na qual o cluster é criado. 

Por exemplo, para ativar o Kibana na região sul dos EUA, navegue para a URL a seguir:

```
Https://logging.ng.bluemix.net/ 
```
{: codeblock}

    
    
## Etapa 3: analisar dados do log no Kibana
{: #step3}

1. Na página **Descobrir**, consulte os eventos que são exibidos. 

    O aplicativo Hello-World de amostra gera um evento.
    
    Na seção Campos disponíveis, é possível ver a lista de campos que podem ser usados para definir novas consultas ou filtrar as entradas listadas na tabela exibida na página.
    
    A tabela a seguir lista os campos comuns que podem ser usados para definir novas consultas de procura. A tabela também inclui valores de amostra que correspondem ao evento que é gerado pelo aplicativo de amostra:
    
     <table>
              <caption>Tabela 2. Campos comuns para logs do contêiner </caption>
               <tr>
                <th align="center">Campo</th>
                <th align="center">Descrição</th>
                <th align="center">Exemplo</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> O valor desse campo corresponde ao GUID do contêiner que executa o app em um pod do cluster do Kubernetes.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>O valor desse campo corresponde à região do {{site.data.keyword.Bluemix_notm}} na qual a entrada de log é coletada.</td>
                <td>Us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>O valor desse campo informa sobre o nome do contêiner.</td>
                <td>Olá a implementação mundial</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>O valor desse campo informa sobre o IP público que está disponível para acessar o app na Internet. </td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>Os campos Rótulo são opcionais. É possível ter 0 ou mais rótulos. Cada rótulo inicia com o prefixo `kubernetes.labels.` Seguido pelo *label_name*. </td>
                <td>No app de amostra, é possível ver 2 rótulos: <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*Kubernetes.namespace_name_str*</td>
                <td>O valor desse campo informa sobre o namespace do Kubernetes no qual o módulo está em execução. </td>
                <td>padrão</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>O valor desse campo corresponde ao GUID do pod no qual o contêiner é executado. </td>
                <td>D695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>O valor desse campo informa sobre o nome do pod.</td>
                <td>Olá mundo a implementação 3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*Mensagem*</td>
                <td>Esta é a mensagem integral registrada pelo aplicativo.</td>
                <td>O aplicativo de amostra está atendendo na porta 8080.</td>
              </tr>
        </table>
    
2. Filtrar dados no **Descobrir** página.  

    Na tabela, é possível ver todas as entradas que estão disponíveis para análise. As entradas listadas correspondem à consulta de procura exibida na barra de Procura. Asterisco (*) é o caractere usado para exibir todas as entradas dentro do período de tempo configurado para a página. 
    
    Por exemplo, para filtrar os dados pelo namespace do Kubernetes, modifique a consulta da barra de Procura. Inclua um filtro com base no campo customizado *kubernetes.namespace_name_str*:
    
    1. Na seção *Campos disponíveis*, selecione o campo *kubernetes.namespace_name_str*. Um subconjunto de valores disponíveis para o campo é exibido.    
    
    2. Selecione o valor **padrão**. Esse é o namespace no qual você implementou em uma etapa anterior o mesmo app.
    
        Após a seleção do valor, um filtro é incluído na barra de Procura e a tabela exibe somente as entradas que correspondem aos critérios recém-selecionados.     
    
    É possível selecionar o símbolo de edição do filtro para modificar o nome do namespace procurado.   
    
    A consulta a seguir exibe:
    
    ```
	{
    "query": {
          "Corresponder": {
            "Kubernetes.namespace_name_str": {
              "query": "default",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Para procurar entradas em um namespace diferente, como *mynamespace1*, modifique a consulta:
    
    ```
	{
    "query": {
          "Corresponder": {
            "Kubernetes.namespace_name_str": {
              "query": "mynamespace1",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Se não for possível ver nenhum dado, tente mudar o filtro de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Para obter mais informações, consulte [Filtrando logs no Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).


## Etapas Seguintes
{: #next_steps}

Em seguida, construa painéis do Kibana. Para obter mais informações, consulte [Analisando logs no Kibana por meio de um painel](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
                                                                                                                      

