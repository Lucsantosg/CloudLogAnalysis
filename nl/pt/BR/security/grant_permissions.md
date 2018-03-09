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


# Concedendo permissões
{: #grant_permissions}

No {{site.data.keyword.Bluemix}}, é possível designar uma ou mais funções para os usuários. Essas funções definem quais tarefas estão ativadas para esse usuário para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}. 
{:shortdesc}



## Designar uma política do IAM a um usuário por meio da UI do {{site.data.keyword.Bluemix_notm}}
{: #grant_permissions_ui_account}

Para conceder a um usuário permissões para visualizar e gerenciar logs de contas, deve-se incluir uma política para esse usuário que descreva as ações que esse usuário pode executar com o serviço {{site.data.keyword.loganalysisshort}} na conta. Somente proprietários da conta podem designar políticas individuais para usuários.

No {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para conceder a um usuário permissões para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Depois de efetuar login com seu ID de usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} é aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Na seção **Políticas de acesso**, clique em **Designar políticas de serviço** e, em seguida, selecione **Designar acesso aos recursos**.

    A janela *Designar acesso a recursos ao usuário** é aberta.

5. Insira informações sobre a política. A tabela a seguir lista os campos que são necessários para definir uma política: 

    <table>
	  <caption>Lista de campos para configurar uma política do IAM.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
	  </tr>
	  <tr>
	    <td>Serviços</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>Regiões</td>
		<td>É possível especificar as regiões nas quais o acesso será concedido ao usuário para trabalhar com logs. Selecione uma ou mais regiões individualmente ou selecione **Todas as regiões atuais** para conceder acesso a todas as regiões.</td>
	  </tr>
	  <tr>
	    <td>Instância de serviço</td>
		<td>Selecione *Todas as instâncias de serviço*.</td>
	  </tr>
	  <tr>
	    <td>Funções</td>
		<td>Selecione uma ou mais funções do IAM. <br>As funções válidas são: *administrador*, *operador*, *editor* e *visualizador*. <br>Para obter mais informações sobre as ações que são permitidas por função, veja [Funções do IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).
		</td>
	  </tr>
     </table>
	
6. Clique em **Designar política**.
	
A política que você configura é aplicável às regiões selecionadas. 

## Designar uma política do IAM a um usuário usando a linha de comandos
{: #grant_permissions_commandline}

Para conceder a um usuário permissões para visualizar e gerenciar logs de contas, deve-se conceder ao usuário uma função do IAM. Para obter mais informações sobre funções do IAM e quais tarefas estão ativadas por função para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}, veja [Funções do IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).

Essa operação pode ser executada somente pelo proprietário da conta.

Conclua as etapas a seguir para conceder a um usuário acesso para visualizar logs de contas usando a linha de comandos:

1. Obtenha o ID da conta. 

    Execute o comando a seguir para obter o ID da conta:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Uma lista de contas com seus GUIDs é exibida.
	
	Exporte o ID da conta da conta na qual você planeja conceder permissões a um usuário para uma variável shell como `$acct_id`, por exemplo:
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. Obtenha o ID do {{site.data.keyword.Bluemix_notm}} do usuário para quem você deseja conceder permissões.

    1. Exiba os usuários que estão associados à conta. Execute o comando a seguir:
	
	    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. Obtenha o GUID do usuário. **Nota:** essa etapa deve ser concluída pelo usuário para quem você planeja conceder permissões.
	
	    Por exemplo, solicite ao usuário para executar os comandos a seguir para obter o ID do usuário:
		
		Obtenha o token do IAM. Para obter mais informações, veja [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

        Obtenha os dados do token do IAM que estão entre os primeiros 2 pontos no token do IAM. Exporte os dados para uma variável shell como `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Execute o comando a seguir, por exemplo, para obter o ID do usuário. Este comando usa jq nessa amostra para decodificar as informações em texto formatado JSON:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		A saída da execução desse comando é a seguinte:
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Envie o ID do usuário para o proprietário da conta.
		
	3. Exporte o ID do usuário para uma variável shell como `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Convide o usuário para a conta se ele ainda não for um membro. Para obter mais informações, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

    Por exemplo, execute o comando a seguir para convidar o usuário xxx@yyy.com para a conta zzz@ggg.com:
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Crie um nome do arquivo de políticas. 

    Por exemplo, use o modelo a seguir para conceder permissões de visualização na região Sul dos EUA:
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-log-analysis",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nomeie o arquivo de políticas: `policy.json`
	
5. Obtenha o token do IAM para seu ID do usuário.

    Para obter mais informações, veja [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

    Exporte o token do IAM para uma variável shell como `$iam_token`, por exemplo:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Conceda ao usuário permissões para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}. 

   Execute o comando cURL a seguir para conceder permissões na região Sul dos EUA:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Execute o comando cURL a seguir para conceder permissões na região do Reino Unido:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
Depois de conceder permissões a um usuário, o usuário pode efetuar login no {{site.data.keyword.Bluemix_notm}} e ver logs de nível de conta.



## Concedendo a um usuário permissões para visualizar logs de espaço usando a UI do {{site.data.keyword.Bluemix_notm}}
{: #grant_permissions_ui_space}

Para conceder a um usuário permissões para visualizar logs em um espaço, deve-se designar ao usuário uma função do Cloud Foundry que descreva as ações que esse usuário pode executar com o serviço {{site.data.keyword.loganalysisshort}} no espaço. 

Conclua as etapas a seguir para conceder a um usuário permissões para trabalhar com o serviço {{site.data.keyword.loganalysisshort}}:

1. Efetue login no console {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	Depois de efetuar login com seu ID de usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} é aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Selecione **Acesso do Cloud Foundry** e, em seguida, selecione a organização.

    Os espaços disponíveis nessa organização estão listados.

5. Escolha um espaço. Em seguida, na ação de menu, selecione **Editar função de espaço**.

6. Selecione 1 ou mais funções de espaço. As funções válidas são: *Gerenciador*, *Desenvolvedor* e *Auditor*
	
7. Clique em **Salvar função**.




