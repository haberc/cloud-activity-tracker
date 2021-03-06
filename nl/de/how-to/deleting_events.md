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


# Ereignisse löschen
{: #deleting_events}

Verwenden Sie den Befehl *ibmcloud at delete*, um Ereignisse, die in {{site.data.keyword.cloudaccesstrailshort}} gespeichert sind, manuell zu löschen.
{:shortdesc}

Führen Sie die folgenden Schritte aus:

## Schritt 1: Bei {{site.data.keyword.Bluemix_notm}} anmelden
{: #prereq}

Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. Führen Sie die folgenden Schritte aus:

1. Melden Sie sich durch Ausführen des Befehls [ibmcloud login](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) bei {{site.data.keyword.Bluemix_notm}} an.
2. Führen Sie den Befehl [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) aus, um festzulegen, für welche Organisation und welchen Bereich (Space) der {{site.data.keyword.cloudaccesstrailshort}}-Service bereitgestellt werden soll.

**Hinweis:** Legen Sie die Organisation und den Bereich (Space) fest, in der bzw. dem {{site.data.keyword.cloudaccesstrailshort}} bereitgestellt wird.

## Schritt 2: Ermitteln, welche Ereignisse verfügbar sind
{: #step2}

Verwenden Sie den Befehl `ibmcloud at status`, um Informationen zu den Ereignissen zu erhalten, die in einer Bereichsdomäne verfügbar sind.

* Um Informationen zu Ereignissen in einer Bereichsdomäne zu erhalten, führen Sie den Befehl `ibmcloud at status` aus.
* Um Informationen zu Ereignissen in der Kontodomäne zu erhalten, führen Sie den Befehl `ibmcloud at status` mit der Option `-a` aus.

Weitere Informationen finden Sie in [Ereignisinformationen anzeigen](/docs/services/cloud-activity-tracker/how-to/viewing_event_information.html#viewing_event_status).
	
  
## Schritt 3: Ereignisse löschen
{: #step3}
	
Führen Sie zum Löschen von Ereignissen den Befehl `ibmcloud at delete` aus.

```
ibmcloud at delete -s YYYY-MM-DD -e YYYY-MM-DD 
```
{: codeblock}
    
Dabei gilt Folgendes:

* *-s* legt das Startdatum in koordinierter Weltzeit (Universal Coordinated Time, UTC) fest: *JJJJ-MM-TT*.
* *-e* legt das Enddatum in koordinierter Weltzeit (Universal Coordinated Time, UTC) fest: *JJJJ-MM-TT*.

Führen Sie zum Beispiel den folgenden Befehl aus, um die Ereignisse für den 10. Juni 2017 zu löschen:

```
ibmcloud at delete -s 2017-06-10 -e 2017-06-10
```
{: screen}

Sie erhalten Informationen zu den Ereignisdatensätzen, die gelöscht wurden.










