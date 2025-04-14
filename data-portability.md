---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-14"

keywords: data portability, compliance, dora

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.instructlab_full_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable you to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, in your location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} provides interfaces and instructions to guide you through the process of copying and storing service customer content, including the related configuration, in your selected location.

You're responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of your application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

To find out more about responsibility ownership for using {{site.data.keyword.cloud}} products between {{site.data.keyword.IBM_notm}} and the customer, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.instructlab_short}} provides the mechanisms to export your content that's uploaded, stored, and processed when you use the service.

The data you process in {{site.data.keyword.instructlab_short}} is stored in an {{site.data.keyword.cos_full_notm}} (COS) instance in your IBM Cloud account.

You can export data from {{site.data.keyword.cos_short}} in the following ways.

- Download objects from your bucket by using the [console](https://cloud.ibm.com/objectstorage){: external}.
- Access the objects in your bucket by using the [COS CLI](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli).
- Access the objects in your bucket by using the `rclone` [CLI tool](/docs/cloud-object-storage?topic=cloud-object-storage-rclone).




## Exported data formats
{: #data-portability-data-formats}

{{site.data.keyword.instructlab_short}} resources are created in several file types including `tar.gz` packages, `.jsonl`, `safetensor`, and `.log` files.

When you export your {{site.data.keyword.instructlab_short}} data from COS, the data in the same format as was originally uploaded.


## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS){: external}.
