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



# Activity Tracker bereitstellen
{: #provision}

Sie können den {{site.data.keyword.cloudaccesstraillong}}-Service über die Benutzerschnittstelle (UI) für {{site.data.keyword.Bluemix}} oder über die Befehlszeile bereitstellen.
{:shortdesc}


## Bereitstellen über die Benutzerschnittstelle (UI)
{: #ui}

Führen Sie die folgenden Schritte aus, um eine Instanz des {{site.data.keyword.cloudaccesstraillong_notm}}-Service in {{site.data.keyword.Bluemix_notm}} bereitzustellen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

    Die Benutzerschnittstelle (UI) für {{site.data.keyword.Bluemix_notm}} finden Sie unter der Adresse [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}.
    
	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie auf **Katalog**. Die Liste der in {{site.data.keyword.Bluemix_notm}} verfügbaren Services wird geöffnet.

3. Wählen Sie die Kategorie **Sicherheit** aus, um die Liste der angezeigten Services zu filtern.

    Der Service ist außerdem in der Kategorie **DevOps** verfügbar.

4. Klicken Sie auf die Kachel **Activity Tracker**.

5. Konfigurieren Sie die entsprechenden Informationen, um zu definieren, wo der Service bereitgestellt werden soll. 

    Geben Sie die Daten ein, wie in der folgenden Tabelle angegeben: 

    <table>
	  <caption>Tabelle 1. Erforderliche Felder zum Bereitstellen des {{site.data.keyword.cloudaccesstrailshort}}-Service</caption>
	  <tr>
	    <th>Feld</th>
		<th>Wert</th>
	  </tr>
	  <tr>
	    <td>Region für die Bereitstellung auswählen:</td>
		<td>Die folgenden Werte sind gültig: Vereinigte Staaten (Süden), Vereinigtes Königreich, Deutschland, Sydney</td>
	  </tr>
	  <tr>
	    <td>Organisation auswählen:</td>
		<td>Wählen Sie die Organisation aus, in der Sie Aktivitäten überwachen möchten.</td>
	  </tr>
	  <tr>
	    <td>Bereich auswählen</td>
		<td>Wählen Sie einen Bereich (Space) in der ausgewählten Organisation aus, für die Sie eine Überwachung der Aktivitäten beabsichtigen.</td>
	  </tr>
	</table>

6. Wählen Sie einen Serviceplan aus. 

    Standardmäßig ist der Plan **Kostenlos** festgelegt.

    Weitere Informationen finden Sie in [Servicepläne](/docs/services/cloud-activity-tracker/how-to/change_plan.html#change_plan).
	
7. Klicken Sie auf **Erstellen**, um den {{site.data.keyword.cloudaccesstrailshort}}-Service in dem {{site.data.keyword.Bluemix_notm}}-Bereich bereitzustellen, bei dem Sie angemeldet sind.
  
 

## Bereitstellen über die CLI
{: #cli}

Führen Sie die folgenden Schritte aus, um eine Instanz des {{site.data.keyword.cloudaccesstrailshort}}-Service in {{site.data.keyword.Bluemix_notm}} über die Befehlszeile bereitzustellen:

1. [Voraussetzung] Installieren Sie die Befehlszeilenschnittstelle (CLI) für {{site.data.keyword.Bluemix_notm}}.

   Weitere Informationen finden Sie in [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) installieren](/docs/cli/reference/ibmcloud/download_cli.html#install_use).
   
   Wenn die CLI installiert ist, fahren Sie mit dem nächsten Schritt fort.
    
2. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. 

    Melden Sie sich durch Ausführen des Befehls [ibmcloud login](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) bei {{site.data.keyword.Bluemix_notm}} an und führen Sie dann den Befehl [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) aus, um festzulegen, für welche Organisation und welchen Bereich (Space) der {{site.data.keyword.cloudaccesstrailshort}}-Service bereitgestellt werden soll.
	
3. Führen Sie den Befehl `ibmcloud service create` aus, um eine Instanz bereitzustellen.

    ```
	ibmcloud service create service_name service_plan service_instance_name
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* 'service_name' ist der Name des Service, d. h. **accessTrail**.
	* 'service_plan' ist der Name des Serviceplans. Eine Liste der Pläne finden Sie in [Servicepläne](/docs/services/cloud-activity-tracker/activity_tracker_ov.html#plan).
	* 'service_instance_name' ist der Name für die neue Serviceinstanz, die Sie erstellen.

	Wenn Sie zum Beispiel eine Instanz des {{site.data.keyword.cloudaccesstrailshort}}-Service mit dem Standardplan erstellen wollen, führen Sie den folgenden Befehl aus:
	
	```
	ibmcloud service create accessTrail free my_activitytracker_svc
	```
	{: codeblock}
	
4. Überprüfen Sie, ob der Service erfolgreich erstellt worden ist. Führen Sie dazu den folgenden Befehl aus:

    ```	
	ibmcloud service list
	```
	{: codeblock}
	
	Die Ausgabe nach dem Ausführen des Befehls sieht wie folgt aus:
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_activitytracker_svc         accessTrail             free                                            create succeeded
	```
	{: screen}

	




