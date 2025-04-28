---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-28"

keywords: taxonomy, troubleshooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `Failed to retrieve taxonomy from COS` error during data generation in {{site.data.keyword.short_name}}
{: #ts-taxonomy-retrieve}


When you try to generate data, you get the following error.
{: tsSymptoms}

```txt
Failed to retrieve taxonomy from COS.
```
{: screen}


The taxonomy TAR file could not be downloaded from {{site.data.keyword.cos_short}}.
{: tsCauses}


Verify that the taxonomy TAR exists in the specified {{site.data.keyword.cos_short}} bucket and that the {{site.data.keyword.cos_short}} authorization policy is still active.
{: tsResolve}


