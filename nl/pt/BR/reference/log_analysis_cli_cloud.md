---

copyright:
  years: 2017, 2018

lastupdated: "2018-03-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# CLI do Log Analysis (plug-in do {{site.data.keyword.Bluemix_notm}})
{: #log_analysis_cli}

A CLI do {{site.data.keyword.loganalysislong}} é um plug-in do {{site.data.keyword.Bluemix_notm}} que pode ser usado para gerenciar os logs armazenados na Coleção de logs.
{: shortdesc}

**Pré-requisitos**
* Antes de executar os comandos de criação de log, efetue login no {{site.data.keyword.Bluemix_notm}} com o comando `bx login` para gerar um token de acesso e autenticar sua sessão.

Para descobrir sobre como usar a CLI do {{site.data.keyword.loganalysisshort}}, veja [Gerenciando logs](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov).

<table>
  <caption>Comandos para gerenciar os logs</caption>
  <tr>
    <th></th>
    <th>Quando utilizá-lo</th>
  </tr>
  <tr>
    <td>[bx logging](#base)</td>
    <td>Use esse comando para obter informações sobre a CLI, como a lista de comandos.</td>
  </tr>
  <tr>
    <td>[bx logging log-delete](#delete)</td>
    <td>Use esse comando para excluir logs armazenados na Coleção de logs.</td>
  </tr>
  <tr>
    <td>[bx logging log-download](#download)</td>
    <td>Use este comando para fazer download de logs da Coleção de logs para um arquivo local ou canalizar os logs para outro programa, como Elastic Stack. </td>
  </tr>
  <tr>
    <td>[bx logging log-show](#status)</td>
    <td>Use esse comando para obter informações sobre os logs que são coletados em um espaço, organização ou conta.</td>
  </tr>
  <tr>
    <td>[bx logging help](#help)</td>
    <td>Use esse comando para obter ajuda sobre como usar a CLI, além de uma lista de todos os comandos.</td>
  </tr>
  <tr>
    <td>[bx logging option-show](#optionshow)</td>
    <td>Use esse comando para visualizar o período de retenção para logs que estão disponíveis em um espaço, organização ou conta.</td>
  </tr>
  <tr>
    <td>[bx logging option-update](#optionupdate)</td>
    <td>Use esse comando para configurar o período de retenção para logs que estão disponíveis em um espaço, organização ou conta.</td>
  </tr>
  <tr>
    <td>[bx logging cota-usage-show](#quotausage)</td>
    <td>Use esse comando para obter as informações de uso de cota para um espaço, uma organização ou uma conta. Também é possível obter as informações de histórico de cota.</td>
  </tr>
  <tr>
    <td>[bx logging session-create](#session_create)</td>
    <td>Use esse comando para criar uma nova sessão.</td>
  <tr>
  <tr>
    <td>[bx logging session-delete](#session_delete)</td>
    <td>Use esse comando para excluir uma sessão.</td>
  <tr>  
  <tr>
    <td>[bx logging sessions](#session_list)</td>
    <td>Use esse comando para listar sessões ativas e seus IDs.</td>
  <tr>  
  <tr>
    <td>[bx logging session-show](#session_show)</td>
    <td>Use esse comando para mostrar o status de uma única sessão.</td>
  <tr>  
  <tr>
    <td>[Bx logging token-get](#tokenget)</td>
    <td>Use esse comando para obter o token de criação de log para enviar dados do log para o serviço {{site.data.keyword.loganalysisshort}}.</td>
  </tr>
</table>


## bx logging
{: #base}

Fornece informações gerais sobre a CLI.

```
bx logging 
```
{: codeblock}

**Exemplos**

Para obter a lista de comandos, execute o comando a seguir:

```
bx logging
NOME:
   bx logging - IBM Cloud Log Analysis Service
USO:
   bx logging command [arguments...] [command options]

COMMANDS:
COMMANDS:
   log-delete         Delete log
   log-download       Download a log
   log-show           Show the count, size, and type of logs per day
   session-create     Create a session
   session-delete     Delete session
   sessions           List sessions info
   session-show       Show a session info
   option-show        Show the log retention
   option-update      Show the log options
   token-get          Get a logging token for sending logs
   quota-usage-show   Show quota usage info
   help             
   
Insira 'bx logging help [command]' para obter mais informações sobre um comando.
```
{: codeblock}




## bx logging log-delete
{: #delete}

Exclui logs armazenados na Coleção de logs.

```
bx logging log-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-f, --force ]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Configura a data de início em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como 2 semanas atrás.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Configura a data de encerramento em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como a data atual.
  </dd>
  
  <dt>-f, --force </dt>
  <dd>(Opcional) Configure essa opção para excluir logs sem precisar confirmar sua ação.
  </dd>
</dl>

**Exemplo**

Para excluir os logs do tipo *linux_syslog* em 25 de maio de 2017, execute o comando a seguir:
```
bx logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: screen}



## bx logging log-download 
{: #download}

Faz download de logs da Coleção de logs em um arquivo local ou canaliza logs para outro programa, como um Elastic Stack. 

**Nota:** para fazer download de arquivos, será necessário criar uma sessão primeiro. Uma sessão define de quais logs fazer download com base no intervalo de data, no tipo de log e no tipo de conta. O download de logs é feito dentro do contexto de uma sessão. Para obter mais informações, veja [bx logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create).

```
 bx logging log-download  [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-o, --output OUTPUT] SESSION_ID

```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
 
  <dt>-o, --output OUTPUT</dt>
  <dd>(Opcional) Configura o caminho e o nome do arquivo para o arquivo de saída local no qual os logs são transferidos por download. <br>O valor padrão é um hífen (-). <br>Configure esse parâmetro como o valor padrão para logs de saída para a saída padrão.</dd>

</dl>

**Argumentos**

<dl>
  <dt>SESSION_ID</dt>
  <dd>Esse valor indica o ID da sessão que se deve usar ao fazer download de logs. <br>**Nota:** o comando `bx logging session-create` fornece os parâmetros que controlam quais logs são transferidos por download. </dd>
</dl>

**Nota:** após a conclusão do download, a execução do mesmo comando novamente recusará a realização de qualquer coisa. Para fazer download dos mesmos dados novamente, deve-se usar um arquivo diferente ou uma sessão diferente.

**Exemplos**

Em um sistema Linux, para fazer download de logs em um arquivo chamado mylogs.gz, execute o comando a seguir:

```
bx logging log-download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

Para fazer download de logs em seu próprio Elastic Stack, execute o comando a seguir:

```
bx logging log-download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
```
{: screen}

O arquivo a seguir é um exemplo de um arquivo logstash.conf:

```
input {
  stdin {
    Codec = > json_lines {
  }
} { {
  Elasticsearch {
    Hosts = > [ "127.0.0.1:9200" ]
  }
}
```
{: screen}


## bx logging help
{: #help}

Fornece informações sobre como usar um comando.

```
bx logging help [command] 
```
{: codeblock}

**Parameters**

<dl>
<dt></dt>
<dd>Configure o nome do comando para o qual você deseja obter ajuda.
</dd>
</dl>


**Exemplos**

Para obter ajuda sobre como executar o comando para visualizar o status de logs, execute o comando a seguir:

```
bx logging help log-show
NOME:
   log-show - Mostrar a contagem, o tamanho e o tipo de logs por dia

USO:
   bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]

OPÇÕES:
   -r, --resource-type     Tipo de recurso, o tipo de recurso válido é conta, organização ou espaço
   -i, --resource-id       ID do recurso, o ID do recurso de destino
   -s, --start             Data de início, o valor do horário UTC incluído no formato AAAA-MM-DD
   -e, --end               Data de encerramento, o valor do horário UTC incluído no formato AAAA-MM-DD
   -t, --type              Tipo de log, por exemplo "syslog"
   -l, --list-type-detail  Listar o tipo detalhado

```
{: screen}


## bx logging option-show
{: #optionshow}

Exibe o período de retenção para logs que estão disponíveis em um espaço, organização ou conta. 

* O período é configurado em número de dias.
* O valor padrão é **-1**. 

**Nota:** por padrão, todos os logs são armazenados. Deve-se excluí-los manualmente usando o comando **delete**. Configure uma política de retenção para excluir os logs automaticamente.

```
bx logging option-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>

</dl>

**Exemplos**

Para ver o período de retenção atual padrão para o espaço no qual você efetuou login, execute o comando a seguir:

```
bx logging option-show
```
{: screen}




## bx logging option-update
{: #optionupdate}

Muda o período de retenção para logs que estão disponíveis em um espaço, organização ou conta. 

* O período é configurado em número de dias.
* O valor padrão é **-1**. 

```
bx logging option-update [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] <-e,--retention RETENTION_VALUE>
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Configure este campo para o ID do espaço, da organização ou da conta para a qual você deseja obter informações. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
  
  <dt>-e,--retention RETENTION_VALUE</dt>
  <dd>Configura o número de dias que os logs são mantidos. </dd>

</dl>

**Exemplo**

Para mudar o período de retenção para 25 dias do espaço ao qual você está conectado, execute o comando a seguir:

```
bx logging option-update -e 25
```
{: screen}


## Bx logging cota-usage-show
{: #quotausage}

Informações sobre o uso de cota de um espaço, uma organização ou uma conta. Também é possível utilizá-lo para obter o uso de histórico.

* O período é configurado em número de dias.
* O valor padrão é **-1**. 

```
bx logging quota-usage-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s,--history]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
  
  <dt>-s, -- histórico</dt>
  <dd>(Opcional) Configure esse parâmetro para obter informações históricas sobre o uso de cota.</dd>

</dl>

**Exemplo**

Para obter o uso de cota histórico para um domínio de espaço, execute o comando a seguir:

```
bx logging quota-usage-show -r space -i js7ydf98-8682-430d-bav4-36b712341744 -s Showing quota usage for resource: js7ydf98-8682-430d-bav4-36b712341744...
OK

Date Allotmant Usage 2018.02.28 524288000 80405926 2018.03.06 524288000 18955540 2018.03.05 524288000 47262944 2018.03.08 524288000 18311338 2018.03.01 524288000 82416831 2018.03.03 524288000 75045462 2018.03.07 524288000 17386278 2018.03.02 524288000 104316444 2018.03.04 524288000 73125223   
```
{: screen}

## bx logging session-create
{: #session_create}

Cria uma nova sessão.

**Nota:** é possível ter até 30 sessões simultâneas em um espaço. A sessão é criada para um usuário. As sessões não podem ser compartilhadas entre usuários em um espaço.

```
bx logging session-create [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Configura a data de início em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como 2 semanas atrás.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Configura a data de encerramento em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como a data atual.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Opcional) Configura o tipo de log. <br>Por exemplo, *syslog* é um tipo de log. <br>O valor padrão é configurado como asterisco (*). <br>É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, *log_type_1,log_type_2,log_type_3*.
  </dd>

</dl>


**Valores Retornados**

<dl>

    <dt>ID</dt>
    <dd>ID de Sessão.</dd>
	
	<dt>Tipo de recurso</dt>
    <dd>ID do recurso.</dd>

    <dt>AccessTime</dt>
    <dd>Registro de data e hora que indica quando a sessão foi usada pela última vez.</dd>

    <dt>CreateTime</dt>
    <dd>O registro de data e hora que corresponde à data e hora em que a sessão foi criada.</dd>
	
	<dt>Iniciar</dt>
    <dd>Indica o primeiro dia que é usado para filtrar logs. </dd>

    <dt>End</dt>
    <dd>Indica o último dia que é usado para filtrar logs.</dd>

    <dt>Tipo</dt>
    <dd>Os tipos de log que são transferidos por download por meio da sessão.</dd>

</dl>


**Exemplo**

Para criar uma sessão que inclua logs para 13 de novembro de 2017, execute o comando a seguir:

```
bx logging session-create -s 2017-11-13 -e 2017-11-13
Creating session for xxxxx@yyy.com resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   2017-11-13   2017-11-13   ANY_TYPE   
Session: 1ef776d1-4d25-4297-9693-882606c725c8 is created
```
{: screen}


## bx logging session-delete 
{: #session_delete}

Exclui uma sessão, especificada pelo ID de sessão.

```
bx session-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
 
</dl>

**Argumentos**

<dl>
  <dt>SESSION_ID</dt>
  <dd>ID da sessão ativa que você deseja excluir.</dd>
</dl>

**Exemplo**

Para excluir uma sessão com o ID de sessão *cI6hvAa0KR_tyhjxZZz9Uw==*, execute o comando a seguir:

```
bx logging session-delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## bx logging sessions
{: #session_list}

Lista as sessões ativas e seus IDs.

```
bx logging sessions [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>

  <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login.  </dd>
</dl>

**Valores de retorno**

<dl>	
    <dt>SESSION_ID</dt>
    <dd>ID da sessão ativa.</dd>
	   
    <dt>ID do recurso</dt>
    <dd>ID do recurso para o qual a sessão é válida.</dd>

    <dt>CreateTime</dt>
    <dd>O registro de data e hora que corresponde à data e hora em que a sessão foi criada.</dd>

    <dt>AccessTime</dt>
    <dd>O registro de data e hora que indica quando a sessão foi usada pela última vez.</dd>
</dl>
 
**Exemplo**

```
bx logging sessions
Listing sessions of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   
Listed the sessions of resource xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
:{ screen}


## bx logging session-show
{: #session_show}

Mostra o status de uma sessão única.

```
bx logging session-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID

```
{: codeblock}

**Parameters**

<dl>
   <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login.  </dd>
</dl>

**Argumentos**

<dl>
   <dt>SESSION_ID</dt>
   <dd>ID da sessão ativa da qual você deseja obter informações.</dd>
</dl>

**Exemplo**

Para mostrar detalhes de uma sessão com ID de sessão *cI6hvAa0KR_tyhjxZZz9Uw==*, execute o comando a seguir:

```
bx logging session-show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}

## Bx logging token-get
{: #tokenget}

Retorna o token de criação de log que é necessário para enviar dados de log para o {{site.data.keyword.loganalysisshort}}.

```
bx logging token-get [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso para o qual você planeja enviar dados de log. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
</dl>


**Exemplo**

```
bx logging token-get -r space -i js7ydf98-8682-430d-bav4-36b712341744
Getting log token of resource: js7ydf98-8682-430d-bav4-36b712341744 ...
OK

Tenant Id                              Logging Token   
js7ydf98-8682-430d-bav4-36b712341744   xxxxxxxxxx   
```
{: screen}


## bx logging log-show
{: #status}

Retorna informações sobre os logs coletados em um espaço ou uma conta do {{site.data.keyword.Bluemix_notm}}.

```
bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]
```
{: codeblock}

* Quando o tipo de recurso não é especificado, o comando retorna os detalhes do recurso no qual você efetuou login.
* Se você especifica um tipo de recurso, deve-se especificar o ID do recurso.
* O comando relata informações somente sobre as últimas 2 semanas de logs que são armazenados na Coleção de logs quando as datas de início e de encerramento não são especificadas.

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Opcional) Configura o tipo de recurso. Os valores válidos são: *space*, *account* e *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Opcional) Defina esse campo para o ID de um espaço, uma organização ou uma conta. <br>Por padrão, se esse parâmetro não for especificado, o comando usará o ID do recurso no qual você efetuou login. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Opcional) Configura a data de início em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como 2 semanas atrás.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Opcional) Configura a data de encerramento em Hora Universal Coordenada (UTC): *AAAA-MM-DD*, por exemplo, `2006-01-02`. <br>O valor padrão é configurado como a data atual.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Opcional) Configura o tipo de log. <br>Por exemplo, *syslog* é um tipo de log. <br>O valor padrão é configurado como asterisco (*). <br>É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>-l, --list-type-detail</dt>
  <dd>(Opcional) Configure esse parâmetro para listar cada tipo de log individualmente.
  </dd>
</dl>


**Exemplo**

```
bx logging log-show
Showing log status of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

Date         Size        Count    Searchable   Types   
2017-11-07   1878197     1333     None         default   
2017-11-13   201653512   179391   All          default,linux_syslog   
2017-11-14   32134119    30425    All          default,linux_syslog   
2017-11-15   303901156   269689   All          linux_syslog,default   
2017-11-16   107253679   96648    All          default,linux_syslog   
```
{: screen}

```
 bx logging log-show -l
Showing log status of resource: cedc73c5-6d55-4193-a9de-378620d6fab5 ...

Date         Size        Count    Searchable   Type   
2017-11-14   30146764    26611    true         default   
2017-11-14   1987355     3814     true         linux_syslog   
2017-11-15   303004895   267890   true         default   
2017-11-15   896261      1799     true         linux_syslog   
2017-11-16   107918249   96278    true         default   
2017-11-16   912890      1794     true         linux_syslog   
```
{: screen}
