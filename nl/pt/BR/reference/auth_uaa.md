---

copyright:
  years: 2017, 2018

lastupdated: "2018-09-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}    
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Obtendo um token da UAA
{: #auth_uaa}

Use o {{site.data.keyword.Bluemix}} UAA para obter um token de autenticação que você possa usar para trabalhar com o serviço {{site.data.keyword.cloudaccesstraillong}}. É possível obter o token de autenticação usando a CLI do {{site.data.keyword.Bluemix_notm}} ou usando APIs.
{:shortdesc}

Considere as informações a seguir:

* O token tem um prazo de expiração. 
* Quando você usa o token, o *Portador* do valor do token deve ser incluído.
		
## Obtendo o token do UAA usando a CLI do IBM Cloud
{: #uaa_cli_token}

Para obter o token do UAA, conclua as etapas a seguir:

1. (Pre-req) Instale a CLI do  {{site.data.keyword.Bluemix_notm}} .

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/ibmcloud/download_cli.html#install_use).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
    
2. Efetue login no  {{site.data.keyword.Bluemix_notm}}. 

    Execute o comando [ibmcloud login](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) para efetuar login no {{site.data.keyword.Bluemix_notm}} e, em seguida, execute o comando [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) para configurar a organização e o espaço nos quais você deseja provisionar o serviço {{site.data.keyword.cloudaccesstrailshort}}.
	
3. Execute o comando `ibmcloud iam oauth-tokens` para obter o token do UAA.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	A saída retorna o token do UAA.


	


## Obtendo o token da UAA para uma chave API da plataforma usando APIs
{: #apikey_uaa_token}

Para obter o token da UAA para uma chave API da plataforma, conclua as etapas a seguir:

1. Obtenha o terminal de autorização. Execute o comando cURL a seguir:

    ```
    curl https://api.ng.bluemix.net/v2/info
    ```
    {: codeblock}

    Na resposta, recupere o valor do terminal no campo **authorization_endpoint**.

2. Inclua uma chave API de plataforma.

    No IBM Cloud Console, navegue para **Gerenciar > Segurança > Chaves API de Plataforma**.
    Em seguida, crie uma Chave API.

3. Obtenha o token. Execute o comando cURL a seguir:

    ```
    curl --user "cf:" --data-urlencode "grant_type=password" --data-urlencode "username=apikey" --data-urlencode "password=$APIKEY" --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" "AUTHORIZATION_ENDPOINT/oauth/token"
    ```
    {: codeblock}

    em que 
    
    *APIKEY* é o valor de apikey obtido em uma etapa anterior.
    
    *AUTHORIZATION_ENDPOINT* representa o ponto de entrada para o serviço do IAM.

    Exemplo:

    ```
    curl --user "cf:" --data-urlencode "grant_type=password" --data-urlencode "username=apikey" --data-urlencode "password=$APIKEY" --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" "https://login.ng.bluemix.net/UAALoginServerWAR/oauth/token"
    ```
    {: codeblock}


