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


# イベントの削除
{: #deleting_events}

*ibmcloud at delete* コマンドを使用して、{{site.data.keyword.cloudaccesstrailshort}} に保管されたイベントを手動で削除します。
{:shortdesc}

以下のステップを実行します。

## ステップ 1: {{site.data.keyword.Bluemix_notm}} にログインする
{: #prereq}

{{site.data.keyword.Bluemix_notm}} にログインします。 以下のステップを実行します。

1. [ibmcloud login](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) コマンドを実行して、{{site.data.keyword.Bluemix_notm}} にログインします。
2. [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) コマンドを実行して、{{site.data.keyword.cloudaccesstrailshort}} サービスをプロビジョンする組織とスペースを設定します。

**注:** {{site.data.keyword.cloudaccesstrailshort}} がプロビジョンされる組織とスペースを設定してください。

## ステップ 2: 使用可能なイベントを識別する
{: #step2}

`ibmcloud at status` コマンドを使用して、スペース・ドメイン内の使用可能なイベントに関する情報を表示します。

* スペース・ドメイン内のイベントに関する情報を取得するには、コマンド `ibmcloud at status` を実行します。
* アカウント・ドメイン内のイベントに関する情報を取得するには、オプション `-a` を指定してコマンド `ibmcloud at status` を実行します。

詳しくは、[イベント情報の表示](/docs/services/cloud-activity-tracker/how-to/viewing_event_information.html#viewing_event_status)を参照してください。
	
  
## ステップ 3: イベントを削除する
{: #step3}
	
イベントを削除するには、コマンド `ibmcloud at delete` を実行します。

```
ibmcloud at delete -s YYYY-MM-DD -e YYYY-MM-DD 
```
{: codeblock}
    
ここで、

* *-s* は、開始日を協定世界時 (UTC) *YYYY-MM-DD* で設定するために使用されます。
* *-e* は、終了日を協定世界時 (UTC) *YYYY-MM-DD* で設定するために使用されます。

例えば、2017 年 6 月 10 日のイベントを削除するには、次のコマンドを実行します。

```
ibmcloud at delete -s 2017-06-10 -e 2017-06-10
```
{: screen}

削除されたイベント・レコードに関する情報が示されます。










