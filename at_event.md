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



# Activity Tracker event fields
{: #at_event}

{{site.data.keyword.cloudaccesstrailshort}} events are based on the Cloud Auditing Data Federation (CADF) standard. 
{:shortdesc}

## Initiator fields
{: #initiator}

The following table list common fields that are available for an {{site.data.keyword.cloudaccesstrailshort}} event:

<table>
  <caption>Common initiator fields</caption>
  <tr>
    <th>Field Name</th>
	  <th>Description</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>initiator.id</td>
	  <td>ID of the initiator of the action. </br>There are two types of initiators: IBMID and serviceID.</td>
    <td>Example of an IBMID: IBMid-000000XXX2 </br>Example of a service ID: iam-ServiceId-12345678-0165-4c89-847d-9660b1632e14</td>
  </tr>
  <tr>
    <td>initiator.name</td>
	  <td>Username of the user that initiated the action.</td>
    <td></td>
  </tr>
  <tr>
    <td>initiator.typeURI</td>
	  <td>Type of the source of the event.</td>
    <td>Valid values are: *service/security/account/user*, *service/security/clientid*, *service/security/account/serviceid*</td>
  </tr>
  <tr>
    <td>initiator.credential.type</td>
	  <td>Type of initiator ID credential. </td>
    <td>Valid values are: *user*, *token*, *apikey*</td>
  </tr>
</table>

## Target fields
{: #target}

The following table list common target fields that are available for an {{site.data.keyword.cloudaccesstrailshort}} event:

<table>
  <caption>Common target fields</caption>
  <tr>
    <th>Field Name</th>
	  <th>Description</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>target.id</td>
	  <td>Cloud Resource Name (CRN) of the resource on which the action is executed. </br>For more information, see [CRN format](/docs/overview/crn.html#format).</td>
    <td>For example: `crn:v1:bluemix:public:cloud-object-storage:global:a/12345678e6232019c6567c9123456789:fr56et47-befb-440a-a223c-12345678dae1:bucket:bucket1`</td>
  </tr>
  <tr>
    <td>target.name</td>
	  <td>Human-readable name of the name of the cloud resource on which the action is executed.</td>
    <td></td>
  </tr>
  <tr>
    <td>target.typeURI</td>
    <td>Type of the cloud resource on which the action is executed. </br>The format of this field is **serviceName/objectType** where servicename is the name of the service. </td>
	  <td>For example: `iam-am/policy` or `cloud-object-storage/bucket/acl`</td>
  </tr>
</table>
 
## Action fields
{: #action}

The following table list common action fields that are available for an {{site.data.keyword.cloudaccesstrailshort}} event:

<table>
  <caption>Common action fields</caption>
  <tr>
    <th>Field Name</th>
	  <th>Description</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>action</td>
	  <td>Action that triggers the event. </br>The format of this field is **serviceName.objectType.action** where servicename is the name of the service. </br>For information about events that are generated by a service, see <a href="/docs/services/cloud-activity-tracker/cloud_services.html#cloud_services">Cloud services</a></td>
    <td>For example: *iam-identity.serviceid-apikey.login*</td>
  </tr>
  <tr>
    <td>eventTime</td>
	  <td>Indicates the timestamp when the event was created. </br>The date is represented as Universal Time Coordinated (UTC). </br>The format complies with ISO 8601.</td>
    <td>For example: 2017-10-19T19:07:50.32+0000<td>
  </tr>
</table>

## Outcome fields
{: #outcomes}

The following table list common outcome fields that are available for an {{site.data.keyword.cloudaccesstrailshort}} event:

<table>
  <caption>Common outcome fields</caption>
  <tr>
    <th>Field Name</th>
	  <th>Description</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>outcome</td>
	  <td>Result of the action. </td>
    <td>Valid values are: *success*, *failure*, *pending*</td>
  </tr>
  <tr>
    <td>reason.reasonCode</td>
	  <td>Numeric field that includes the HTTP response code. </td>
    <td>For example, *200* for a successful outcome.</td>
  </tr>
  <tr>
    <td>severity</td>
	  <td>Defines the level of threat an action may have on the Cloud.  </td>
    <td>Valid values are: *normal*, *warning*, and *critical* </br></br>**Normal** is set for routine actions in the Cloud. For example: starting an instance, or refreshing a token. </br></br>**Warning** is set for actions where a Cloud resource is updated or its metadata is modified. For example: updating the version of a worker node, renaming a certificate, or renaming a service instance. </br></br>**Critical** is set for actions that affect security in the Cloud. For example: changing credentials of a user, deleting data, unauthorized access to work with a Cloud resource. </td>
  </tr>
</table>
