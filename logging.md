---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-01"

keywords: instructlab, logging, logs routing

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Logging for {{site.data.keyword.instructlab_short}}
{: #logging}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.instructlab_short}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems. Logs are generated in each region where {{site.data.keyword.short_name}} is available.
{: shortdesc}

## Enabling logging
{: #log-enable}

To enable logging, create an instance of {{site.data.keyword.logs_full_notm}}. For more information, see [Getting started with IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-getting-started).

## Setting up {{site.data.keyword.atracker_short}}
{: #at-event-routing}

After you have an instance of {{site.data.keyword.logs_full_notm}}, you can route user activity to that instance by setting it as a target in {{site.data.keyword.atracker_short}}. For more information, see [Configuring an {{site.data.keyword.logs_full_notm}} instance as a target](/docs/atracker?topic=atracker-getting-started-target-cloud-logs&interface=ui).

{{_include-segments/actions.md}}

## Viewing logs
{: #log-viewing}

You can view logs in the [Observability console](https://cloud.ibm.com/observability/logging).

You can find {{site.data.keyword.short_name}} logs by using the following query.
```txt
message:"instructlab\:"
```
{: codeblock}

You can use the following query to find all `critical` events for `instructlab`.
```txt
message:"instructlab\:" AND _exists_:"severity"
```
{: codeblock}

You can all events from a specific user by using the following query and replacing `name@email.com` with the user's email address.
```txt
message:"instructlab\:" AND initiator.name:"name@email.com"
```
{: codeblock}

For more information, see [About platform logs](/docs/logs-router?topic=logs-router-about-platform-logs).
