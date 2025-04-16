---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-16"

keywords: instructlab, ai, project

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Creating storage locations for {{site.data.keyword.short_name}}
{: #storage}

Complete the following steps to create one or more {{site.data.keyword.cos_short}} buckets to store {{site.data.keyword.short_name}} resources in.
{: shortdesc}

[Learn more about {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage).


## Creating an {{site.data.keyword.cos_short}} instance and bucket by using the CLI
{: #storage-cli}
{: cli}

To log in:
{{_include-segments/login.md}}

To create {{site.data.keyword.cos_short}} resources:
1. [Create a new bucket](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#create-a-new-bucket) and make a note of the bucket name for later.
    ```sh
    ibmcloud cos bucket-create --bucket <bucket-name> [--class <class-name>] [--ibm-service-instance-id <instance-id>] [--region REGION] [--output FORMAT]
    ```
    {: pre}
