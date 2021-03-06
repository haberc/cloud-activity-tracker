---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Suppression d'informations sur les événements
{: #deleting_events_api}

Utilisez l'API {{site.data.keyword.cloudaccesstrailshort}} pour supprimer les événements qui sont stockés dans {{site.data.keyword.cloudaccesstrailshort}}.
{:shortdesc}

**Remarque :** bien que vous puissiez supprimer des événements manuellement à l'aide de l'appel API, envisagez de définir la règle de conservation pour supprimer des événements automatiquement. Pour plus d'informations, voir [Configuration de la règle de conservation des événements](/docs/services/cloud-activity-tracker/how-to/configuring_retention_policy.html#configuring_retention_policy). 

## Suppression d'événements à l'aide de cURL
{: #records_per_day_curl}

Procédez comme suit pour supprimer les événements qui sont disponibles dans un domaine d'espace :

1. Obtenez un jeton UAA. 

    Pour plus d'informations, voir [Obtention d'un jeton UAA](/docs/services/cloud-activity-tracker/reference/auth_uaa.html#auth_uaa).

2. Exécutez la commande cURL suivante pour supprimer les événements qui sont stockés dans {{site.data.keyword.cloudaccesstrailshort}} à une date spécifique. 

    ```
    curl -H  "Content-Type:application/json" -H "X-Auth-Token: bearer ${token}" -H "X-Auth-Project-Id:${spaceId}" -H "Accept:application/json" -X DELETE  ENDPOINT/v3/events -d '{"start":"2018-06-24","end":"2018-06-24","AtAccountLevel":false,"SearchTime":""}'
    ```
    {: codeblock}

    où

    * *token* est le jeton UAA. 
    * *spaceID* représente l'identificateur unique universel de l'espace Cloud Foundry où {{site.data.keyword.cloudaccesstrailshort}} est mis à disposition. 
    * *ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour obtenir la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-activity-tracker/reference/ref_endpoints.html#api_endpoints). 
    * *start* et *end* représentent la plage de temps pendant laquelle vous souhaitez télécharger des événements. Le format de date est AAAA-MM-JJ. 
    * *AtAccountLevel* indique le domaine dans lequel vous voulez obtenir des informations sur les événements.
    * *SearchTime* indique l'heure de la journée pour laquelle vous souhaitez des informations sur les événements.


Par exemple, pour supprimer les événements d'un jour spécifique dans un domaine d'espace dans la région Sud des Etats-Unis, vous pouvez exécuter la commande cURL suivante : 

```
curl -H  "Content-Type:application/json" -H "X-Auth-Token: bearer ${token}" -H "X-Auth-Project-Id:${spaceId}" -H "Accept:application/json" -X DELETE  https://activity-tracker.ng.bluemix.net/v3/events -d '{"start":"2018-06-24","end":"2018-06-24","AtAccountLevel":false,"SearchTime":""}'
```
{: codeblock}

Par exemple, pour supprimer les événements de la semaine dernière dans un domaine d'espace, vous pouvez exécuter la commande cURL suivante : 

```
curl -H  "Content-Type:application/json" -H "X-Auth-Token: bearer ${token}" -H "X-Auth-Project-Id:${spaceId}" -H "Accept:application/json" --request DELETE --data "{\"start\":\"$(date -u -v-7d +%F)\", \"end\":\"$(date -u -v-6d +%F)\" }" https://activity-tracker.ng.bluemix.net/v3/events
```
{: codeblock}


## Exemple NodeJS de suppression d'événements
{: #node}

Il s'agit du code exemple que vous pouvez utiliser pour tester la suppression d'événements :

L'exemple suppose que le service {{site.data.keyword.cloudaccesstrailshort}} est mis à disposition dans la région Sud des Etats-Unis.  

```
var http = require("https")
var fs = require("fs")

var token = "{TOKEN}";

// ID de l'espace Cloud Foundry où le service {{site.data.keyword.cloudaccesstrailshort}} est mis à disposition.
var spaceId = "{SPACE_ID}";

var endDate = "2018-07-02";
var startDate = "2018-06-30";

var http = require("https");

var options = {
    "method": "DELETE",
    "connection": "close",
    "hostname": "activity-tracker.ng.bluemix.net",
    "port": null,
    "path": "/v3/events",
    "headers": {
        "x-auth-token": token,
        "x-auth-project-id": spaceId,
        "accept": "application/json",
        "content-type": "application/json"
    }
};

var req = http.request(options, function (res) {
    var chunks = [];

    res.on("data", function (chunk) {
        chunks.push(chunk);
    });

    res.on("end", function () {
        var body = Buffer.concat(chunks);
        console.log(body.toString());
    });
});

req.write(JSON.stringify({
    end: endDate,
    start: startDate
}));
req.end();
```
{: codeblock}
