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


# Obtendo o token do UAA
{: #auth_uaa}

Para gerenciar logs usando a API do {{site.data.keyword.loganalysisshort}}, deve-se usar um token de autenticação. Use a CLI do {{site.data.keyword.loganalysisshort}} para obter o token do UAA. O token tem um tempo de expiração. 
{:shortdesc}

		
## Obtendo o token do UAA usando a CLI do Log Analysis (plug-in do CF)
{: #uaa_cli}


Para obter o token de autorização, conclua as etapas a seguir:

1. Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, veja [Fazer download e instalar a CLI do {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
    
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Execute o comando `bx cf oauth-token` para obter o token do UAA do {{site.data.keyword.Bluemix_notm}}.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	A saída retorna o token UAA que se deve usar para autenticar seu ID do usuário nesse espaço e nessa organização.
	

**Nota:** Ao usar o token, remova *Bearer* do valor do token que você passa em uma chamada API.
