---
layout: article
title: Single sign-on with Azure
permalink: /user-guide/users/single-sign-on/azure-sso.html
flags:
  admin: true
  logzio-plan: pro
tags:
  - sso
  - azure
contributors:
  - schwin007
---

Single sign-on is available for Enterprise plans.
To discuss switching to an Enterprise plan, please contact your account manager.

#### To set up single sign-on for Azure

<div class="tasklist">

##### Request SSO access from Logz.io

Only account admins can request single sign-on access for their accounts.
{:.info-box.note}

To kick off this process, send an email to [help@logz.io](mailto:help@logz.io).
Write that you want to set up Azure SAML SSO for Logz.io.
Include these items in the message:

* Your Logz.io account ID
* Your [account token](https://app.logz.io/#/dashboard/settings/manage-accounts)

The Support team will respond with the connection information you'll need to give in Azure.

##### Add Logz.io to Azure

![Add a non-gallery application in Azure]({{site.baseurl}}/images/sso-providers/azure/add-your-own-application.png)

In the [Azure Portal](https://portal.azure.com/), browse to **Azure Active Directory  > Enterprise Applications > New application > Non-gallery application**.

In the right panel, set the **Name** to "Logz.io" and click **Add**.

Click **Configure Single Sign-On**, and choose **SAML-based Sign-on**.

##### Paste the SAML information from Support

![Add a non-gallery application in Azure]({{site.baseurl}}/images/sso-providers/azure/configure-single-sign-on.png)

Fill in these details from the Logz.io Support email message:

* In **Identifier (Entity ID)**, paste _Audience URI_ from the email
* In **Reply URL (Assertion Consumer Service URL)**, paste _Single sign on URL_ from the email

##### Zip the SAML certificate

In the SAML Signing Certificate section of the page, click the **Certificate (Base64)** download link (next to the certificate).

Download the certificate file and zip it.
You'll attach this zip file to your next email to the Support team.

Save your configuration.

##### Get your endpoint information

Browse to **Azure Active Directory > App registrations > Endpoints**.

Copy the **SAML-P SIGN-ON ENDPOINT**, and paste this in the email that you'll send to the Support team.

##### Send your SAML details to Logz.io

Draft a new [email to Support](mailto:help@logz.io), and include these items:

* Your zipped certificate (from step 4)
* Your SAML-P SIGN-ON ENDPOINT (from step 5)

##### Configure Azure to send user groups

Return to the App registrations page.
If you don't see Logz.io, click **View all applications**.

Open the **Logz.io** application, and then click **Manifest**.
In the manifest JSON, set groupMembershipClaims to `"All"`.
Click **Save** (top of the page).

##### _(Optional)_ Restrict Logz.io access to specific user groups

![Add group]({{site.baseurl}}/images/access-and-authentication/sso--manage-groups.png)

By default, all Azure users with Logz.io access can sign in to your Logz.io accounts.

You can restrict this access from the [Manage users page](https://app.logz.io/#/dashboard/settings/manage-users) for each of your accounts.
To do this, click **Add group**, and then paste your group's Object ID from Azure.
Do this for each group that should have access to this account.

##### Receive confirmation from Support

When Support has created your Azure + Logz.io connection, you're done!
You can start logging in to Logz.io through your Apps portal.

</div>
