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

# Tutorial Introdução
{: #getting-started-with-cla}

Use este tutorial para saber como começar a trabalhar com o serviço {{site.data.keyword.loganalysislong}} no {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Objetivos
{: #objectives}

* Provisione o serviço {{site.data.keyword.loganalysislong}} em um espaço.
* Configure a linha de comandos para gerenciar logs.
* Configure permissões para um usuário visualizar logs em um espaço.
* Ative o Kibana, a ferramenta de software livre que pode ser usada para visualizar logs.


## Antes de iniciar
{: #prereqs}

Deve-se ter um ID de usuário que seja membro ou proprietário de uma conta do {{site.data.keyword.Bluemix_notm}}. Para obter um ID de usuário do {{site.data.keyword.Bluemix_notm}}, acesse: [Registro ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/registration/){:new_window}

Este tutorial fornece instruções para provisionar e trabalhar com o serviço {{site.data.keyword.loganalysisshort}} na região sul dos EUA.


## Etapa 1: Provisionar o serviço {{site.data.keyword.loganalysisshort}}
{: #step1}

**Nota:** você provisiona uma instância do serviço {{site.data.keyword.loganalysisshort}} em um espaço do Cloud Foundry (CF). Só é necessária uma instância do serviço por espaço. Não é possível provisionar o serviço {{site.data.keyword.loganalysisshort}} no nível de conta. 

Conclua as etapas a seguir para provisionar uma instância do serviço {{site.data.keyword.loganalysisshort}} no {{site.data.keyword.Bluemix_notm}}:

1. Efetue login no {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}.  

2. Selecione a região, a organização e o espaço nos quais você deseja provisionar o serviço {{site.data.keyword.loganalysisshort}}.  

3. Clique em **Catálogo**. A lista dos serviços que estão disponíveis no {{site.data.keyword.Bluemix_notm}} é aberta.

4. Selecione a categoria **DevOps** para filtrar a lista de serviços exibida.

5. Clique no quadro **Análise do log**.

6. Selecione um plano de serviço. Por padrão, o plano **Lite** é configurado.

    Para obter mais informações sobre os planos de serviços, veja [Planos de serviços](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
7. Clique em **Criar** para provisionar o serviço {{site.data.keyword.loganalysisshort}} no espaço do {{site.data.keyword.Bluemix_notm}} ao qual você está conectado.




## Etapa 2: [Opcional] Mudar o plano de serviço para o serviço {{site.data.keyword.loganalysisshort}}
{: #step2}

Se você precisar de mais cota de procura, armazenamento de longo prazo de logs ou ambos, será possível mudar seu plano de instância de serviço do {{site.data.keyword.loganalysisshort}} por meio da UI do {{site.data.keyword.Bluemix_notm}} ou executando o comando `bx cf update-service` para ativar esses recursos. 

É possível fazer upgrade ou reduzir o plano de serviço a qualquer momento.

Para obter mais informações, veja [Planos de serviço do {{site.data.keyword.loganalysisshort}}](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

**NOTA:** a mudança do plano para um plano pago tem um custo.

Para mudar o plano de serviço na UI do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}.  

2. Selecione a região, a organização e o espaço em que o serviço do {{site.data.keyword.loganalysisshort}} está disponível.  

3. Clique na instância de serviço do {{site.data.keyword.loganalysisshort}} no *Painel* do {{site.data.keyword.Bluemix_notm}}. 
    
4. Selecione a guia **Plano** no painel {{site.data.keyword.loganalysisshort}}.

    São exibidas informações sobre o seu plano atual.
	
5. Selecione um novo plano para fazer upgrade ou reduzir o seu plano. 

6. Clique em **Salvar**.



## Etapa 3: Configurar seu ambiente local para funcionar com o serviço {{site.data.keyword.loganalysisshort}}
{: #step3}


O serviço {{site.data.keyword.loganalysisshort}} inclui uma interface da linha de comandos (CLI) que pode ser usada para gerenciar logs armazenados na Coleção de logs (componente de armazenamento de longo prazo). 

É possível usar o plug-in {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} para visualizar o status do log, fazer download de logs e configurar a política de retenção de log. 

A CLI oferece diferentes tipos de ajuda: ajuda geral para aprender sobre a CLI e os comandos suportados, ajuda de comando para aprender como usar um comando ou ajuda de subcomando para aprender como usar um subcomando para um comando.

Para instalar a CLI do {{site.data.keyword.loganalysisshort}} por meio do repositório do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, veja [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Instale o plug-in {{site.data.keyword.loganalysisshort}}. Execute o comando a seguir:

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. Verifique se o plug-in do {{site.data.keyword.loganalysisshort}} está instalado.
  
    Por exemplo, execute o comando a seguir para ver a lista de plug-ins que estão instalados:
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    A saída é semelhante ao seguinte:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## Etapa 4: Configurar permissões para um usuário visualizar logs
{: #step4}

Para controlar as ações do {{site.data.keyword.loganalysisshort}} que um usuário tem permissão para executar, é possível designar funções e políticas para um usuário. 

Há dois tipos de permissões de segurança no {{site.data.keyword.Bluemix_notm}} que controlam as ações que os usuários podem executar ao trabalharem com o serviço {{site.data.keyword.loganalysisshort}}:

* Funções do Cloud Foundry (CF): você concede a um usuário uma função do CF para definir as permissões que o usuário tem para visualizar logs em um espaço.
* Funções do IAM: você concede a um usuário uma política do IAM para definir as permissões que o usuário tem para visualizar logs no domínio de contas, além das permissões que o usuário tem para gerenciar logs armazenados na Coleção de logs. 


Conclua as etapas a seguir para conceder a um usuário permissões para visualizar logs em um espaço:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Depois de efetuar login com seu ID de usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} é aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Selecione **Acesso do Cloud Foundry** e, em seguida, selecione a organização.

    Os espaços disponíveis nessa organização estão listados.

5. Escolha o espaço no qual você provisionou o serviço {{site.data.keyword.loganalysisshort}}. Em seguida, na ação de menu, selecione **Editar função de espaço**.

6. Selecione *Auditor*. 

    É possível selecionar 1 ou mais funções de espaço. Todas as funções a seguir permitem que um usuário visualize logs: *Gerenciador*, *Desenvolvedor* e *Auditor*
	
7. Clique em **Salvar função**.


Para obter mais informações, veja [Concedendo permissões](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).



## Etapa 5: Ativar o Kibana
{: #step5}

Para visualizar e analisar dados do log, deve-se acessar o Kibana na região Pública da nuvem na qual os dados do log estiverem disponíveis. 


Para ativar o Kibana na região sul dos EUA, abra um navegador da web e insira a URL a seguir:

```
Https://logging.ng.bluemix.net/ 
```
{: codeblock}


Para obter mais informações sobre como ativar o Kibana em outras regiões, veja [Navegando para o Kibana por meio de um navegador da web](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

**Nota:** quando você ativar o Kibana, se receber uma mensagem indicando *token de acesso não válido*, verifique suas permissões no espaço. Essa mensagem é uma indicação de que seu ID de usuário não tem permissões para ver logs.
    

## Etapas Seguintes 
{: #next_steps}

Gerar logs. Tente um dos tutoriais a seguir:

* [Analisar logs no Kibana para um app que é implementado em um cluster do Kubernetes](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    Esse tutorial demonstra as etapas necessárias para obter o seguinte cenário de ponta a ponta funcionando: provisionar um cluster, configurar o cluster para enviar logs para o serviço {{site.data.keyword.loganalysisshort}} no {{site.data.keyword.Bluemix_notm}}, implementar um app no cluster e usar o Kibana para visualizar e filtrar logs do contêiner para esse cluster.     
    
* [Analisar logs no Kibana para um app Cloud Foundry](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    Esse tutorial demonstra as etapas necessárias para obter o seguinte cenário de ponta a ponta funcionando: implementar um aplicativo Python Cloud Foundry, gerar tipos diferentes de logs e usar o Kibana para visualizar, procurar e analisar logs do CF.
   








