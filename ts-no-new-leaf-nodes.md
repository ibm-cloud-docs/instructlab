---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-28"

keywords: leaf node, taxonomy, trouble shooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `No new leaf nodes found in the taxonomy` error when generating data in {{site.data.keyword.short_name}}
{: #ts-no-new-leaf-nodes}

When you try to generate data, you get the following error.
{: tsSymptoms}

```txt
Generating dataset failed with the following error: Error: No new leaf nodes found in the taxonomy.
```
{: screen}

The error is likely related to an issue with the `tar.gz` file that contains your taxonomy, especially if you are using Windows or any non-UNIX based operating system. The `ibmcloud ilab taxonomy add` command is compatible with UNIX systems. For other operating systems, an additional step might be necessary to upload your taxonomy.
{: tsCauses}

Another reason could be that the taxonomy did not include QNA files within it.

Use GitHub to generate a new [`tar.gz` file](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases){: external}. Then, use the IBM Cloud UI to upload the `tar.gz` file.
{: tsResolve}

1. Use GitHub to [create a new release for your taxonomy and generate a `tar.gz` file](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases){: external}. Download the `tar.gz` file. 

2. Navigate to the [{{site.data.keyword.short_name}} UI](https://cloud.ibm.com/instructlab/overview){: external} and click `Add taxonomy`.

3. In the `Upload taxonomy` menu, upload the new `tar.gz` file into your {{site.data.keyword.cos_short}} bucket. 

4. Try to [generate data](/docs/instructlab?topic=instructlab-data-generate&interface=ui). 
