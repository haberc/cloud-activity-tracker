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


# Supresión de sucesos
{: #deleting_events}

Utilice el mandato *ibmcloud at delete* para suprimir manualmente los sucesos que están almacenados en {{site.data.keyword.cloudaccesstrailshort}}.
{:shortdesc}

Siga estos pasos:

## Paso 1: Iniciar sesión en {{site.data.keyword.Bluemix_notm}}
{: #prereq}

Inicie una sesión en {{site.data.keyword.Bluemix_notm}}. Siga estos pasos:

1. Ejecute el mandato [ibmcloud login](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) para iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.
2. Ejecute el mandato [ibmcloud target](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) para definir la organización y el espacio donde desea suministrar el servicio {{site.data.keyword.cloudaccesstrailshort}}.

**Nota:** establezca la organización y el espacio donde se suministra {{site.data.keyword.cloudaccesstrailshort}}.

## Paso 2: Identificar los sucesos que están disponibles
{: #step2}

Utilice el mandato `ibmcloud at status` para ver información sobre los sucesos que están disponibles en un dominio del espacio.

* Para obtener información sobre los sucesos de un dominio del espacio, ejecute el mandato `ibmcloud at status`.
* Para obtener información sobre los sucesos en el dominio de la cuenta, ejecute el mandato `ibmcloud at status` con la opción `-a`.

Para obtener más información, consulte [Visualización de la información de sucesos](/docs/services/cloud-activity-tracker/how-to/viewing_event_information.html#viewing_event_status).
	
  
## Paso 3: Suprimir sucesos
{: #step3}
	
Para suprimir sucesos, ejecute el mandato `ibmcloud at delete`.

```
ibmcloud at delete -s YYYY-MM-DD -e YYYY-MM-DD 
```
{: codeblock}
    
donde

* *-s* se utiliza para establecer la fecha de inicio en Hora Universal Coordinada (UTC): *AAAA-MM-DD*.
* *-e* se utiliza para establecer la fecha final en Hora Universal Coordinada (UTC): *AAAA-MM-DD*.

Por ejemplo, para suprimir sucesos del 10 de junio de 2017, ejecute el siguiente mandato:

```
ibmcloud at delete -s 2017-06-10 -e 2017-06-10
```
{: screen}

Recibirá información sobre los registros de sucesos que se han suprimido.










