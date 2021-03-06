---

copyright:
  years: 2016, 2018
lastupdated: "2018-11-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Monitoring {{site.data.keyword.BluVirtServers_short}} and {{site.data.keyword.baremetal_short}} with {{site.data.keyword.cloudaccesstrailshort}}
{: #vsi}

Use this tutorial to learn how to configure users in an {{site.data.keyword.Bluemix_notm}} account so that those users can manage infrastructure devices that are created by using {{site.data.keyword.BluVirtServers_short}} and {{site.data.keyword.baremetal_short}}, and the users actions generate {{site.data.keyword.cloudaccesstrailshort}} events that you can monitor by using {{site.data.keyword.cloudaccesstrailshort}}.
{:shortdesc}

{{site.data.keyword.BluVirtServers}} are scalable virtual servers that are purchased with dedicated cores and memory allocations. They are a great option if you are looking for compute resources, that can be added in minutes, with access to features like image templates. 
* For more information, see [{{site.data.keyword.BluVirtServers_short}} ](/docs/vsi/vsi_about.html#about-virtual-servers). 
* For the list of actions that generate an {{site.data.keyword.cloudaccesstrailshort}} event, see [Events generated by {{site.data.keyword.BluVirtServers_short}}](/docs/vsi/vsi_activity_tracker_events.html#at_events).

{{site.data.keyword.baremetal_short}} are single-tenant physical servers that provide you performance and control with low-level access to the hardware resources. 
* For more information, see [{{site.data.keyword.baremetal_long}} ](/docs/bare-metal/about.html#about).
* For the list of actions that generate an {{site.data.keyword.cloudaccesstrailshort}} event, see [Events generated by {{site.data.keyword.baremetal_short}}](/docs/bare-metal/bm-activity-tracker-events.html#at_events).

**For a user to generate {{site.data.keyword.BluVirtServers_short}} and {{site.data.keyword.baremetal_short}} {{site.data.keyword.cloudaccesstrailshort}} events, the user must have access to Infrastructure resources in the IBM Cloud Console.**
{: tip}

## Step 1: Link the Softlayer account to an {{site.data.keyword.Bluemix_notm}} account
{: #step1}

** To generate {{site.data.keyword.cloudaccesstrailshort}} events, the Softlayer account must be linked to an {{site.data.keyword.Bluemix_notm}} account. For more information, see [Switching to IBMid and linking accounts](/docs/account/softlayerlink.html#link_user_accounts).

Consider the following information when linking your Softlayer account to an {{site.data.keyword.Bluemix_notm}} account:
* All new accounts automatically receive an IBMid and existing SoftLayer accounts, except SAML federated accounts, are enabled to switch to IBMid authentication.
* Each SoftLayer account that you plan to link to an {{site.data.keyword.Bluemix_notm}} account must be owned by a unique IBMid with a unique email address.
* To switch your existing SoftLayer account to an IBMid, you create an IBMid and then use your registration code to confirm it.
* After an account is switched to an IBMid account, you can link the SoftLayer account and the {{site.data.keyword.Bluemix_notm}} account to use combined infrastructure as a service (IaaS) and platform as a service (PaaS) resources. 

Complete the following steps to link an account:
1. [Request an IBMid and registration code](/docs/account/softlayerlink.html#reqIBMidandregcode)
2. [Confirm your IBMid with the registration code](/docs/account/softlayerlink.html#confIBMiduseregcode)
3. [Link your IBMid account](/docs/account/softlayerlink.html#link_user_account)


## Step 2: Grant users infrastructure permissions
{: #step2}

**Note:** If you grant permissions from the *{{site.data.keyword.Bluemix_notm}} Infrastructure Portal*, the user does not have access from the *{{site.data.keyword.Bluemix_notm}} Infrastructure* dashboard to manage devices and {{site.data.keyword.cloudaccesstrailshort}} events are not generated. **You must grant a user infrastruture permissions through the {{site.data.keyword.Bluemix_notm}} account to manage devices. These actions generate {{site.data.keyword.cloudaccesstrailshort}} events.**
{: tip}

Complete the following steps to grant a user infrastructure permissions:

1. Log in to the {{site.data.keyword.Bluemix_notm}}.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.
    
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage** &gt; **Account**, and then select **Users**. 

3. Choose a user to whom you want to grant permissions to work with devices.

4. Select **Assign access**.

5. Select **Assign access to your Softlayer account**. The {{site.data.keyword.Bluemix_notm}} Infrastructure Portal opens within the context of the {{site.data.keyword.Bluemix_notm}}.

6. Set the permissions that you want to grant the user to manage devices. Select **Portal permissions**. Then, in the **Devices** section, grant the user the permissions that the user needs to manage devices. For example: *View Virtual Server Details*, *Reboot server and view IPMI system information*, *Upgrade Server*, or *Issue OS Reloads and Initiate Rescue Kernel*.

7. Save the portal permissions. When you select **Device Access**, you are prompted to save the changes. Click **Save**.

8. Set the devices that the user can manage. In the **Device Access** section, select the physical devices. Then, click **Update Device Access**.





