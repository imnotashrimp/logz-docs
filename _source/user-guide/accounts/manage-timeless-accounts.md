---
layout: article
title: Manage timeless accounts
permalink: /user-guide/accounts/manage-timeless-accounts.html
flags:
  admin: true
  logzio-plan: pro
tags:
  - accounts
  - timeless-accounts
contributors:
  - imnotashrimp
  - ayigal
---

While your main account and sub accounts
are better suited for short-term monitoring of your log data,
they're not really a cost-effective way to view long-term patterns and trends.
That's where timeless accounts come in.

Timeless accounts work with optimizers,
allowing you to save a subset of your logs for as long as you need them.
You can store key metrics that you want to track in your timeless accounts.
Each timeless account contains its own Elasticsearch index,
which you can search from your main account.

![Timeless accounts]({{site.baseurl}}/images/accounts/accounts--timeless-accounts.png)

#### To create or manage a timeless account

<div class="tasklist">

##### Select or add a timeless account

In the **Timeless account plan** panel,
click the timeless account you want to manage,
or click **Add timeless account**.

![Manage a timeless account]({{site.baseurl}}/images/accounts/accounts--manage-timeless-account.png)

##### Adjust account volume

If you need to adjust the **Timeless account volume**,
type in the text box
or use <i class="li li-plus"></i> and <i class="li li-minus"></i>.

Your plan allows for a maximum data volume.
Keep this limit in mind when you allocate resources to your timeless accounts—you won't be able to exceed the limits of your plan. \\
\\
Contact your Logz.io account manager if you need to increase your plan limits.
{:.info-box.note}

##### Set search permissions

If you want your sub accounts to be able to search this account,
add the intended accounts to the **Read & write permissions** box.

##### Save your changes

Click **Apply** to save your changes.

</div>