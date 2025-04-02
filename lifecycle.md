---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-02"

keywords: instructlab

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Understanding the lifecycle policy for {{site.data.keyword.instructlab_short}}
{: #lifecycle-policy}

Review this page for general information about {{site.data.keyword.instructlab_short}} versions.
{: shortdesc}

{{site.data.keyword.cloud_notm}} makes it easy for you to access and take advantage of the latest capabilities within our services across the platform. By doing this, we recognize that it might take time to migrate or upgrade workloads to the latest releases, so we provide lifecycle guidelines to help you. {{site.data.keyword.cloud_notm}} is committed to communicating the lifecycle and versioning guidelines for support throughout the life of the {{site.data.keyword.cloud_notm}} service, so you have plenty of time to plan for the future. For detailed information, review the [IBM changes to cloud services document](https://www.ibm.com/support/customer/csol/terms/?id=i126-6605&lc=en){: external}.

## Version numbering
{: #version-numbering}

The following types of versioning apply to {{site.data.keyword.instructlab_short}}.

Service version
:   Each update is documented in a change log and follows the RHEL AI distribution version. It is named in the format of `x.y.z-patch`, where `x.y.z` is the RHEL AI version and the `patch` is the build patch version from IBM Cloud. For example, `1.4.1-1`.

CLI version
:   Each release uses semantic version where the version is named in the format of `x.y.z`, where `x` is the major version number, `y` is the minor version number, and `z` is the patch number. For example, `0.0.16`. If the major version number increments, it indicates that the new version contains significant changes comparing to the previous version. You can find the CLI version, by running the `ibmcloud ilab` command.

API version
:   Each release uses semantic version where the version is named in the format of `x.y.z`, where `x` is the major version number, `y` is the minor version number, and `z` is the patch number. For example, `1.0`. This version can be found in the [API document](https://us-east.instructlab.ibm.com/swagger-instructlab-api/swagger.yaml){: external}.

## {{site.data.keyword.instructlab_short}} recommended and supported versions
{: #ilab-service-version}

Provide the recommended version, supported version, and version policy for your service if applicable. See the following example:

{{site.data.keyword.instructlab_short}} offers the following versions that can be ordered today or are coming soon if their General Availability (GA) date is in the future. We include an End of Support (EOS) date too, where this is known. To help you plan for the future, we aim to provide up to 12 month's notice of a version going to End of Support (EOS), though the actual time between notification and our EOS date will depend on EOS notice provided by third party vendors or open source communities. {{site.data.keyword.cloud_notm}} will not provide third party software or services that are not supported by the third party.

| Service | Version | GA date | EOS procedure |
|----|----|----|----|
| {{site.data.keyword.instructlab_short}} | 1.4 | 10 March 2025 | Automatically upgraded in place to next Major version|
{: caption="Recommended and supported version types for {{site.data.keyword.instructlab_short}}" caption-side="bottom"}

## Customer communications for {{site.data.keyword.instructlab_short}}
{: #customer-communications}

{{site.data.keyword.cloud_notm}} recommends that you stay up to date with the latest news and announcements for {{site.data.keyword.instructlab_short}}, as well as for {{site.data.keyword.cloud_notm}} in general, by using the following resources:

- [IBM Cloud Announcements](https://cloud.ibm.com/status/announcement){: external}
- [IBM Announcements](https://www.ibm.com/think){: external}
- [End of support notices](https://cloud.ibm.com/status/announcement?query=End+of+Support+Notices){: external}
- [Red Hat Product Life Cycles](https://access.redhat.com/product-life-cycles/){: external}

## Other considerations
{: #other-considerations-lifecycle}

Use this section to describe other details to consider for your service.  
