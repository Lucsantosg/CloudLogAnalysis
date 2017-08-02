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

# Configurando a política de retenção de log
{: #configuring_retention_policy}

Use o comando **cf logging option** para visualizar e configurar a política de retenção que define o número máximo de dias que os logs são mantidos na Coleção de logs. Por padrão, os logs são mantidos por 30 dias. Após a expiração do período de retenção, os logs são excluídos automaticamente. Por padrão, a política de retenção fica desativada.
{:shortdesc}

É possível ter políticas de retenção diferentes definidas na conta. É possível ter uma política de conta global e políticas de espaço individuais. A política de retenção configurada no nível de conta define o número máximo de dias durante os quais é possível manter os logs. Se você configurar uma política de retenção de espaço para um período de tempo superior ao período de nível de conta, a política aplicada será a última política configurada para esse espaço. 


## Desativando a política de retenção de log de um espaço
{: #disable_retention_policy_space}

Conclua as etapas a seguir para desativar uma política de retenção:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja configurar uma política de retenção de log. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Configure o período de retenção como **-1** para desativar o período de retenção. Execute o comando:

    ```
    Cf log opção -r -1
    ```
    {: codeblock}
    
**Exemplo**
    
Por exemplo, para desativar o período de retenção de um espaço com o ID *d35da1e3-b345-475f-8502-cfgh436902a3*, execute o comando a seguir:

```
Cf log opção -r -1
```
{: codeblock}

A saída é:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen} 



## Verificando a política de retenção de log de um espaço
{: #check_retention_policy_space}

Para obter o período de retenção configurado para um espaço do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja configurar uma política de retenção de log. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Sai o período de retenção. Execute o comando:

    ```
    cf logging option
    ```
    {: codeblock}

    A saída é:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Verificando a política de retenção de log de todos os espaços em uma conta
{: #check_retention_policy_account}

Para obter o período de retenção configurado para cada espaço do {{site.data.keyword.Bluemix_notm}} em uma conta, conclua as etapas a seguir:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja configurar uma política de retenção de log. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenha o período de retenção de cada espaço na conta. Execute o comando:

    ```
    Cf criação de opção -a
    ```
    {: codeblock}

    A saída é:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    | fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Configurando uma política de retenção de log no nível de conta
{: #set_retention_policy_space}

Para ver o período de retenção de uma conta do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja configurar uma política de retenção de log. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Configure o período de retenção. Execute o comando:

    ```
    cf logging option -r *Number_of_days* - a
    ```
    {: codeblock}
    
    em que *Number_of_days* é um número inteiro que define o número de dias que você deseja manter os logs. 
    
    
**Exemplo**
    
Por exemplo, para manter qualquer tipo de log em sua conta por 15 dias apenas, execute o comando a seguir:

```
Cf log opção -r 15 -a
```
{: codeblock}

A saída lista uma entrada de cada espaço na conta, incluindo informações sobre o período de retenção:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        15 |
+--------------------------------------+-----------+
| fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
+--------------------------------------+-----------+
```
{: screen}

## Configurando a política de retenção de log de um espaço
{: #set_retention_policy_account}

Para ver o período de retenção de um espaço do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja configurar uma política de retenção de log. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Configure o período de retenção. Execute o comando:

    ```
    Cf log opção -r *Number_of_days *
    ```
    {: codeblock}
    
    em que *Number_of_days* é um número inteiro que define o número de dias que você deseja manter os logs.
    
    
**Exemplo**
    
Por exemplo, para manter os logs disponíveis em um espaço por um ano, execute o comando a seguir:

```
Cf log opção -r 365
```
{: codeblock}

A saída é:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |       365 |
+--------------------------------------+-----------+
```
{: screen}


