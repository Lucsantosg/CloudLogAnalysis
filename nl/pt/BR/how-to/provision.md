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


# Provisionando o serviço de análise do log
{: #provision}

É possível provisionar o serviço {{site.data.keyword.loganalysisshort}} por meio da UI do {{site.data.keyword.Bluemix}} ou por meio da linha de comandos.
{:shortdesc}


## Provisionando por meio da UI
{: #ui}

Conclua as etapas a seguir para provisionar uma instância do serviço {{site.data.keyword.loganalysisshort}} no {{site.data.keyword.Bluemix_notm}}:

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.

    O painel do {{site.data.keyword.Bluemix_notm}} pode ser localizado em: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net "Ícone de link externo"){:new_window}.
    
	Depois de efetuar login com seu ID de usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} é aberta.

2. Clique em **Catálogo**. A lista dos serviços que estão disponíveis no {{site.data.keyword.Bluemix_notm}} é aberta.

3. Selecione a categoria **DevOps** para filtrar a lista de serviços exibida.

4. Clique no quadro **Análise do log**.

5. Selecione um plano de serviço. Por padrão, o plano **Lite** é configurado.

    Para obter mais informações sobre os planos de serviços, veja [Planos de serviços](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
6. Clique em **Criar** para provisionar o serviço {{site.data.keyword.loganalysisshort}} no espaço do {{site.data.keyword.Bluemix_notm}} ao qual você está conectado.
  
 

## Provisionando por meio da CLI
{: #cli}

Conclua as etapas a seguir para provisionar uma instância do serviço {{site.data.keyword.loganalysisshort}} no {{site.data.keyword.Bluemix_notm}} por meio da linha de comandos:

1. Instale a CLI do Cloud Foundry (CF). Se o CF CLI estiver instalado, continue com a próxima etapa.

   Para obter mais informações, veja [Instalando o cf CLI ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Ícone de link externo"){: new_window}. 
    
2. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:

    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Siga as instruções. Insira suas credenciais do {{site.data.keyword.Bluemix_notm}}, selecione uma organização e um espaço.
	
3. Execute o comando `cf create-service` para provisionar uma instância.

    ```
	cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}
	
	Em que
	
	* service_name é o nome do serviço, isto é, **ibmLogAnalysis**.
	* service_plan é o nome do plano de serviço. Para obter uma lista de planos, veja [Planos de serviços](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	* service_instance_name é o nome que você deseja usar para a nova instância de serviço criada.
	
	Para obter mais informações sobre o comando cf, veja [cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service).

	Por exemplo, para criar uma instância do serviço {{site.data.keyword.loganalysisshort}} com um plano grátis, execute o comando a seguir:
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}
	
4. Verifique se o serviço foi criado com sucesso. Execute o comando a seguir:

    ```	
	cf services
	```
	{: codeblock}
	
	A saída da execução do comando é semelhante ao seguinte:
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	{

	



