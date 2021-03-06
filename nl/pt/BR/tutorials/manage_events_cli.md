---

copyright:
  years: 2016, 2018
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



# Gerenciando eventos usando a CLI do Activity Tracker
{: #tutorial2}

Use este tutorial para aprender como usar a CLI do {{site.data.keyword.cloudaccesstrailshort}} para gerenciar eventos por meio da linha de comandos. Saiba como obter informações sobre eventos armazenados, como fazer download de eventos que são armazenados no {{site.data.keyword.IBM_notm}} Cloud ou como excluir eventos.
{:shortdesc}

Conclua
as etapas a seguir:

1. [Provisione o {{site.data.keyword.keymanagementservicelong_notm}} e gere eventos](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step1)
2. [Obtenha informações sobre eventos armazenados (ibmcloud at status)](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step2)
2. [Especifique de quais logs fazer download criando uma sessão (ibmcloud at session create)](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step3)
3. [Obtenha os dados do log reais (ibmcloud at download)](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step4)
4. [Exclua a sessão após a conclusão do download (ibmcloud at session delete)](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step5)
5. [Exclua manualmente os logs que não são necessários (ibmcloud at delete)](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html#step6)


## Suposições
{: #assumptions}

1. Você tem um ID do usuário do {{site.data.keyword.Bluemix_notm}} que tem permissões de desenvolvedor para trabalhar em um espaço de uma conta do {{site.data.keyword.Bluemix_notm}} na qual o serviço {{site.data.keyword.cloudaccesstrailshort}} é provisionado. 

    Para obter mais informações sobre como provisionar o serviço {{site.data.keyword.cloudaccesstrailshort}}, veja [Provisionando o serviço {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/how-to/provision.html#provision).

2. Você provisionou uma instância do serviço {{site.data.keyword.cloudaccesstrailshort}} com um plano premium.

    **Nota:** a CLI do {{site.data.keyword.cloudaccesstrailshort}} não está disponível com o plano Lite.

3. Você instalou a CLI do {{site.data.keyword.cloudaccesstrailshort}} em seu sistema local. Isso é necessário para que seja possível usar a CLI do {{site.data.keyword.cloudaccesstrailshort}} para gerenciar eventos por meio da linha de comandos. 

    Para obter mais informações sobre como instalar a CLI do {{site.data.keyword.cloudaccesstrailshort}}, veja [Configurando a CLI do {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/how-to/config_cli.html#config_cli).

4. Você efetuou login no {{site.data.keyword.Bluemix_notm}} por meio da linha de comandos. Para esse tutorial, execute os comandos a seguir em um terminal: 

    `ibmcloud login -a api.ng.bluemix.net` para efetuar login na região us-south. Para obter mais informações, consulte  [ login ibmcloud ](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login).
    
    `ibmcloud target -o OrgName -s SpaceName` para configurar a organização de destino e o espaço em que o serviço {{site.data.keyword.cloudaccesstrailshort}} é provisionado. Para obter mais informações, consulte [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target).


## Etapa 1: provisionar o serviço IBM Key Protect e gerar eventos 
{: #step1}
	
Conclua as etapas a seguir para provisionar o serviço {{site.data.keyword.keymanagementserviceshort}} no {{site.data.keyword.Bluemix_notm}} e gerar eventos:

1. Provisione uma instância do serviço {{site.data.keyword.keymanagementserviceshort}} na região Sul dos EUA. Para obter mais informações, consulte [Provisionando por meio do console do IBM Cloud](/docs/services/key-protect/provision.html#provision).

2. Defina as permissões do {{site.data.keyword.Bluemix_notm}} para o usuário que você está planejando usar para trabalhar com chaves. 

    * Um usuário precisa de uma política do IAM com uma função de serviço configurada como *manager* ou *writer* para que possa criar chaves.
	* Um usuário precisa de uma política do IAM com uma função de serviço configurada como *manager* para que possa excluir chaves.
	* Um usuário precisa de uma política do IAM com uma função de serviço configurada como *reader* para que possa ver chaves. 

3. Crie uma chave de segurança usando o serviço {{site.data.keyword.keymanagementserviceshort}} para gerar os dados do evento do {{site.data.keyword.cloudaccesstrailshort}}. Para obter mais informações, consulte [Criando novas chaves](/docs/services/key-protect/create-standard-keys.html#create-standard-keys).

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} são gerados como resultado da criação de uma chave.

## Etapa 2: obter informações sobre eventos armazenados
{: #step2}

Os eventos do {{site.data.keyword.keymanagementserviceshort}} estão disponíveis no domínio de contas do
{{site.data.keyword.cloudaccesstrailshort}}.

Nesse tutorial, os eventos do {{site.data.keyword.keymanagementserviceshort}} estão disponíveis no domínio de contas Sul dos EUA que é a região na qual você provisionou o serviço do {{site.data.keyword.keymanagementserviceshort}}. 

Execute o comando a seguir para obter informações sobre eventos coletados em uma data específica:

```
ibmcloud at status -s startDate -e endDate -a
```
{: codeblock}

em que 

* `-s` é usado para configurar o dia de início. 
* ` startDate `  representa a data de início. O formato é  * YYYY-MM-DD *.
* `-e` é usado para configurar a data de encerramento.
* ` endDate `  representa a data de encerramento. O formato é  * YYYY-MM-DD *.
* `-a` é usado para indicar para incluir eventos no domínio de contas.

Exemplo:

```
ibmcloud at status -s 2017-07-25 -e 2017-07-25 -a
+------------+-------+-------+------------+
| Date       | Count | Size  | Searchable |
+------------+-------+-------+------------+
| 2017-07-25 | 12    | 34994 | All        |
+------------+-------+-------+------------+
```
{: screen}

Esse comando contará os eventos para 25 de junho de 2017.  {{site.data.keyword.cloudaccesstrailshort}} é um serviço global, portanto, os dias são em Horário Universal. Para obter um dia de horário local completo, você provavelmente precisará fazer download de múltiplos dias de UTC.




## Etapa 3: especificar de quais eventos fazer download
{: #step3}

Antes de fazer download de eventos, crie uma sessão. A sessão especifica quais eventos serão transferidos por download.


Use o comando a seguir para criar uma sessão:

```
ibmcloud at session create -s startDate -e endDate -a
```
{: codeblock}

em que 

* `-s` é usado para configurar o dia de início. 
* ` startDate `  representa a data de início. O formato é  * YYYY-MM-DD *.
* `-e` é usado para configurar a data de encerramento.
* ` endDate `  representa a data de encerramento. O formato é  * YYYY-MM-DD *.
* `-a` é usado para indicar para incluir eventos no domínio de contas.

Exemplo:

```
ibmcloud at session create -s 2017-07-25 -e 2017-07-25 -a
+--------------+-------------------------------------------+
| Name         | Value                                     |
+--------------+-------------------------------------------+
| id           | 21b19aeb-3d32-4c60-b912-517609c62db2      |
| space        | 667fb895-b5f5-46c9-9f0e-cf4587341095      |
| username     | xxx@yyy.com                               |
| create-time  | 2017-07-25T18:33:22.678350874Z            |
| access-time  | 2017-07-25T18:33:22.678350874Z            |
| date-range   | {"End":"2017-07-25","Start":"2017-07-25"} |
| type-account | {"Type":"ActivityTracker"}                |
+--------------+-------------------------------------------+
```
{: screen}

em que 

* `-s` é usado para configurar o dia de início.
* `-e` é usado para configurar a data de encerramento.
* `-a` é usado para indicar para incluir eventos no domínio de contas.

Há uma data de início e uma data de encerramento associadas a uma sessão. O comando de download incluirá eventos entre essas datas inclusivas.

A parte importante da saída do comando é o `Id` de sessão. Ele é referenciado no comando de download.

Para obter informações sobre as sessões existentes, digite `ibmcloud at session list`.

Para saber mais sobre as sessões e o comando `ibmcloud at session create`, consulte a [Referência da CLI](/docs/services/cloud-activity-tracker/reference/at_cli_cloud.html#session_create).

Use `ibmcloud at session help create` para obter ajuda na linha de comandos.

## Etapa 4: fazer download de eventos que são identificados para o escopo definido para a sessão
{: #step4}

Para fazer download dos eventos especificados pelos parâmetros de sessão, execute o comando a seguir:

```
ibmcloud at events download -o outputFile sessionID
```
{: codeblock}

* O parâmetro `-o` especifica um arquivo de saída.
* `outputFile` é o nome do arquivo local.
* O `sessionID` é especificado por último. Você obterá o valor do ID de sessão na saída do comando `ibmcloud at session create`.

O formato dos dados transferidos por download é compactado como JSON. 

Exemplo:

```
$ ibmcloud at events download -o events.log 21b19aeb-3d32-4c60-b912-517609c62db2
 6.70 KiB / 3.06 KiB [================================================================================================================================================================] 219.03% 8.60 MiB/s 0s
Download Successful
```
{: screen} 

O indicador de progresso é movido de 0 a 100% conforme os eventos são transferidos por download.

Para saber mais sobre o comando `ibmcloud at download`, consulte a [Referência da CLI](/docs/services/cloud-activity-tracker/reference/at_cli_cloud.html#download).

Use `ibmcloud at help download` para obter ajuda na linha de comandos.

## Etapa 5: excluir a sessão
{: #step5}

Após a conclusão do download, exclua a sessão. Execute o seguinte comando:

```
ibmcloud at session delete sessionID
```
{: codeblock}

em que 

* `sessionID` é o ID da sessão que você deseja excluir.

O número de sessões é limitado. Uma sessão não é excluída automaticamente. Deve-se excluir manualmente as sessões que não são necessárias. 

Exemplo: 

```
$ ibmcloud at session delete 21b19aeb-3d32-4c60-b912-517609c62db2
+---------+------------------------+
| name    | value                  |
+---------+------------------------+
| message | Delete session success |
+---------+------------------------+
```
{: screen}

Para saber mais sobre o comando `ibmcloud at session delete`, consulte a [Referência da CLI](/docs/services/cloud-activity-tracker/reference/at_cli_cloud.html#session_delete).

Use `ibmcloud at session help delete` para obter ajuda na linha de comandos.

## Etapa 6: excluir eventos do Activity Tracker automaticamente
{: #step6}

Você tem controle de sua própria retenção de eventos no {{site.data.keyword.cloudaccesstrailshort}}. É possível excluir eventos manualmente ou automatizar a exclusão de eventos.

Para excluir eventos manualmente de um espaço, execute o comando `ibmcloud at delete`. Por
exemplo,

```
$ ibmcloud at delete -s 2017-07-25 -e 2017-07-25
Deleted successfully
"6 logs were deleted,freeing 13737 bytes."
```

Para saber mais sobre o comando `ibmcloud at delete`, consulte a [Referência da CLI](/docs/services/cloud-activity-tracker/reference/at_cli_cloud.html#delete).

Use `ibmcloud at help delete` para obter ajuda na linha de comandos.

**Nota:** para excluir eventos automaticamente, é possível configurar uma política de retenção usando o comando da CLI `ibmcloud at option`. Para obter mais informações, veja [Referência da CLI](/docs/services/cloud-activity-tracker/reference/at_cli_cloud.html#option)


