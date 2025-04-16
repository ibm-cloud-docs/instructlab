---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-16"

keywords: responsibilities, rhel ai, instructlab

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.instructlab_full_notm}}
{: #responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.instructlab_full_notm}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.instructlab_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud}} Terms and Notices](/docs/overview?topic=overview-terms).


## Incident and operations management
{: #incident-and-ops}

Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

| Area | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Logging | {{site.data.keyword.IBM_notm}} responsibility description  | Create an instance of {{site.data.keyword.logs_full_notm}} and configure the instance to receive {{site.data.keyword.short_name}} logs. Review logs and take action as needed. |
| Tracking user activity | Send activity tracking events to   | Create an instance of {{site.data.keyword.logs_full_notm}} and configure the instance to receive {{site.data.keyword.atracker_short}} events from {{site.data.keyword.short_name}} logs. Review user events and take action as needed. |
{: row-headers}
{: caption="Responsibilites for incident and operations" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}



## Identity and access management
{: #iam-responsibilities}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.


| Area | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| User permissions | Align with the IAM controls documented for the IAM operations a client can perform at the service and platform level. | Manage IAM policies with users to give them proper access to use the service based on their needs. |
| Object Storage permissions | Use service delegation to read, write, and list objects within the Object Storage specified when adding a taxonomy. | Give InstructLab authorization to allow operations on the Object Storage bucket. Revoke the permissions if they're no longer using the service. |
{: row-headers}
{: caption="Responsibilites for identity and access management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}
