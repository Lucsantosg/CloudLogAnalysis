---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Segurança
{: #security_ov}

Para controlar as ações do {{site.data.keyword.loganalysisshort}} que um usuário tem permissão para executar, é possível designar uma ou mais funções a um usuário. 
{:shortdesc}

Para trabalhar com a API do serviço {{site.data.keyword.loganalysisshort}}, você precisa usar um token do UAA ou um token do IAM. Para enviar logs para o serviço {{site.data.keyword.loganalysisshort}}, você precisa de um token de criação de log.


## Modelos de Autenticação
{: #auth}

Para trabalhar com o serviço {{site.data.keyword.loganalysisshort}} por meio da CLI ou API, você precisa de um token de autenticação.

O serviço {{site.data.keyword.loganalysisshort}} suporta os modelos de autenticação a seguir:

* [Autenticação do UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)

    É possível usar a CLI apenas para gerenciar tokens do UAA.
	
* [Autenticação do IAM](/docs/services/CloudLogAnalysis/security/auth_iam.html#auth_iam)

    O modelo de autenticação do IAM oferece recursos de gerenciamento de UI, CLI ou API. 

**Nota:** um token do UAA e um token do IAM expiram após um período de tempo. 

## Funções
{: #roles}

Há dois tipos de funções no {{site.data.keyword.Bluemix_notm}} que controlam as ações que os usuários podem executar quando eles trabalham com o serviço {{site.data.keyword.loganalysisshort}}:

* Funções do Cloud Foundry (CF): você controla quais ações do {{site.data.keyword.loganalysisshort}} um usuário pode executar, designando uma ou mais funções do CF. Com essas funções, você controla as permissões do usuário para visualizar e gerenciar logs em um espaço ou em uma organização.
* Funções do IAM: você controla as ações do {{site.data.keyword.loganalysisshort}} que um usuário pode executar designando uma ou mais funções do IAM. Com essas funções, você controla as permissões do usuário para visualizar e gerenciar logs de contas. 


A tabela a seguir lista o tipo de funções e o domínio no {{site.data.keyword.Bluemix_notm}} que elas controlam:

<table>
  <caption>Tabela 1. Tipo de funções que controlam as ações por domínio</caption>
  <tr>
    <th></th>
	<th align="right">Conta</th>
    <th align="right">Organização</th>
    <th align="right">Espaço</th>	
  </tr>
  <tr>
    <td align="left">Funções do CF</td>
	<td align="center">Não</td>
	<td align="center">Sim</td>
	<td align="center">Sim</td>
  </tr>
  <tr>
    <td align="left">Funções IAM</td>
	<td align="center">Sim</td>
	<td align="center">Não</td>
	<td align="center">Não</td>
  </tr>
</table>


## Funções do CF
{: #bmx_roles}

A tabela a seguir lista os privilégios de cada uma das funções do CF para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}:

<table>
  <caption>Tabela 2. Funções e privilégios do Cloud Foundry para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}.</caption>
  <tr>
    <th>Função</th>
	<th>Domínio</th>
	<th>Privilégios de acesso</th>
  </tr>
  <tr>
    <td>Gerente</td>
	<td>Organização <br>Espaço</td>
	<td>Todas as APIs RESTful</td>
  </tr>
  <tr>
    <td>Desenvolvedor</td>
	<td>Espaço</td>
	<td>Todas as APIs RESTful</td>
  </tr>
  <tr>
    <td>Auditor</td>
	<td>Organização <br>Espaço</td>
	<td>Somente as APIs RESTful que executam operações somente leitura, como logs de consulta.</td>
  </tr>
</table>


## Funções IAM
{: #iam_roles}

A tabela a seguir lista os privilégios de cada uma das funções do IAM para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}:

<table>
  <caption>Tabela 3. Funções e privilégios do IAM para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}.</caption>
  <tr>
    <th>Função</th>
	<th>Privilégios</th>
  </tr>
  <tr>
    <td>Administrator</td>
	  <td>Visualize informações sobre os logs em um espaço ou no nível de conta. <br>Faça download de logs em um arquivo log ou canalize os logs para outro programa, como Elastic Stack. <br>Exibe o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Atualiza o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Lista as sessões ativas e seus IDs. <br>Crie uma sessão que pode ser usada para fazer download de logs. <br>Exclua uma sessão especificada pelo ID de sessão. <br>Mostra o status de uma sessão única. <br>Exclua logs. </td>
  </tr>
  <tr>
    <td>Editor</td>
	  <td>Visualize informações sobre os logs em um espaço ou no nível de conta. <br>Faça download de logs em um arquivo log ou canalize os logs para outro programa, como Elastic Stack. <br>Exibe o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Atualiza o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Lista as sessões ativas e seus IDs. <br>Crie uma sessão que pode ser usada para fazer download de logs. <br>Exclua uma sessão especificada pelo ID de sessão. <br>Mostra o status de uma sessão única. <br>Exclua logs.  </td>
  </tr>
  <tr>
    <td>Operador</td>
	  <td>Visualize informações sobre os logs em um espaço ou no nível de conta. <br>Exibe o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Lista as sessões ativas e seus IDs. <br>Mostra o status de uma sessão única. <br>Faça download de logs em um arquivo log ou canalize os logs para outro programa, como Elastic Stack.  <br>Crie uma sessão que pode ser usada para fazer download de logs. <br>Exclua uma sessão especificada pelo ID de sessão. </td>
  </tr>
  <tr>
    <td>Viewer</td>
	  <td>Visualize informações sobre os logs em um espaço ou no nível de conta. <br>Exibe o período de retenção para logs que estão disponíveis em um espaço ou conta. <br>Lista as sessões ativas e seus IDs. <br>Mostra o status de uma sessão única. </td>
  </tr>
</table>

A tabela a seguir lista o relacionamento entre a API, uma ação de serviço e uma função do IAM que é usada pelo serviço {{site.data.keyword.loganalysisshort}}.

<table>
  <caption>Tabela 4. Relacionamento entre a API, uma ação de serviço e uma função do IAM. </caption>
  <tr>
    <th>API</th>
	<th>Ação</th>
	<th>Função IAM</th>
	<th>Descrição</th>
  </tr>
  <tr>
    <td>DELETE /v1/logging/logs</td>
    <td>ibmcloud-log-analysis.domain.log_delete</td>
	<td>Administrador, Editor</td>
	<td>Exclua logs.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs</td>
    <td>ibmcloud-log-analysis.domain.log_read</td>
	<td>Administrador, Editor, Visualizador</td>
	<td>Visualize informações sobre os logs em um espaço do {{site.data.keyword.Bluemix_notm}} ou no nível de conta.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs/download</td>
    <td>ibmcloud-log-analysis.domain.log_download</td>
	<td>Administrador, Editor</td>
	<td>Faça download de logs em um arquivo log ou canalize os logs para outro programa, como Elastic Stack.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs/retention</td>
    <td>ibmcloud-log-analysis.domain.policy_read</td>
    <td>Administrador, Editor, Visualizador</td>
    <td>Exibe o período de retenção para os logs que estão disponíveis em um espaço ou conta do {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  <tr>
    <td>PUT /v1/logging/logs/retention</td>
    <td>ibmcloud-log-analysis.domain.policy_write</td>
    <td>Administrador, Editor</td>
    <td>Atualiza o período de retenção para logs que estão disponíveis em um espaço ou conta do {{site.data.keyword.Bluemix_notm}}.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/sessions</td>
    <td>ibmcloud-log-analysis.domain.session_read</td>
    <td>Administrador, Editor, Visualizador</td>
    <td>Lista as sessões ativas e seus IDs.</td>
  </tr>
  <tr>
    <td>POST /v1/logging/sessions</td>
    <td>ibmcloud-log-analysis.domain.session_write</td>
    <td>Administrador, Editor</td>
    <td>Crie uma sessão que pode ser usada para fazer download de logs.</td>
  </tr>
  <tr>
    <td>DELETE /v1/logging/sessions/{id}</td>
    <td>ibmcloud-log-analysis.domain.session_delete</td>
    <td>Administrador, Editor</td>
    <td>Exclua uma sessão especificada pelo ID de sessão.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/sessions/{id}</td>
    <td>ibmcloud-log-analysis.domain.session_read</td>
    <td>Administrador, Editor, Visualizador</td>
    <td>Mostra o status de uma sessão única.</td>
  </tr>
</table>

## Obtendo um token de autenticação para gerenciar os logs usando a API
{: #get_token}

Para gerenciar logs usando a API do {{site.data.keyword.loganalysisshort}}, deve-se usar um token de autenticação. 

**Trabalhando com logs que estão disponíveis no domínio de espaço**

* Use a CLI do {{site.data.keyword.loganalysisshort}} para obter o token do UAA. 
* O token tem um tempo de expiração. 

Para obter mais informações, veja [Obtendo o token do UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

**Trabalhando com logs que estão disponíveis no domínio de contas**

* Use a CLI do {{{site.data.keyword.Bluemix_notm}} para obter o token do IAM. 
* O token tem um tempo de expiração. 

Para obter mais informações, veja [Obtendo o token do IAM](/docs/services/CloudLogAnalysis/security/auth_iam.html#auth_iam).


## Obtendo o token de criação de log para enviar logs para o Log Analysis
{: #get_logging_token}

Para enviar logs para o serviço {{site.data.keyword.loganalysisshort}}, você precisa de um token de criação de log. 

Para enviar logs para um domínio de espaço, escolha um dos métodos a seguir:

* [Obtendo o token de criação para enviar logs para um espaço usando o comando bx service do {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/logging_token.html#logging_token_cloud_cli)
* [Obtendo o token de criação para enviar logs para um espaço usando a CLI do Log Analysis (plug-in do CF)](/docs/services/CloudLogAnalysis/security/logging_token.html#logging_token_cf_plugin)
* [Obtendo o token de criação para enviar logs para um espaço usando a API do Log Analysis](/docs/services/CloudLogAnalysis/security/logging_token.html#logging_token_api)

Para enviar logs para o domínio de contas, veja [Obtendo o token de criação de log para enviar logs para o domínio de contas usando a API do Log Analysis](/docs/services/CloudLogAnalysis/security/logging_token.html#logging_acc_token_api).



## Concedendo permissões para um usuário para trabalhar com logs
{: #grant_permissions}

Para que um usuário possa gerenciar logs ou visualizar logs, o usuário deve receber permissões no {{site.data.keyword.Bluemix_notm}} para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}.

* Para obter informações sobre as permissões necessárias para gerenciar os logs, veja [Funções que são necessárias para um usuário para gerenciar os logs](/docs/services/CloudLogAnalysis/manage_logs.html#roles).
* Para obter informações sobre as permissões necessárias para visualizar logs, veja [Funções que são necessárias para um usuário para visualizar logs](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#roles).

Para obter mais informações sobre como conceder permissões, veja:

* [Designar uma política do IAM para um usuário por meio da UI do {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions).
* [Designar uma política do IAM para um usuário usando a linha de comandos](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_commandline).
* [Concedendo a um usuário permissões de usuário para visualizar logs de espaço usando a UI do {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space).

