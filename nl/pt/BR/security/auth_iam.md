---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Obtendo o token do IAM
{: #auth_iam}

Para gerenciar os logs que estão disponíveis no domínio de contas usando a API do {{site.data.keyword.loganalysisshort}}, deve-se usar um token de autenticação. Use a CLI do {{{site.data.keyword.Bluemix_notm}} para obter o token do IAM. O token tem um tempo de expiração. 
{:shortdesc}


## Obtendo o token do IAM
{: #iam_token_cli}

Para obter o token de autorização usando a CLI do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir em um terminal:

1. Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, veja [Fazer download e instalar a CLI do {{site.data.keyword.Bluemix}}](/docs/cli/index.html#overview).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
    
2. Efetue login em uma região no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Execute o comando `ibmcloud iam oauth-tokens` para obter o token IAM.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	A saída retorna o token IAM que se deve usar para autenticar seu ID do usuário nesse espaço e nessa organização. É possível exportar o token do IAM para uma variável shell, como `$iam_token`.



**Nota:** ao usar o token, remova *Bearer* do valor do token que for passado em uma chamada API.

